# Longhorn

## Overview 
* Distributed block storage


## Architecture

* `Manager` runs on each node creating/ managing volumes, handle API calls (also from Longhorn UI)
* `Engine instance` for each volume running on attached node and node where there's a volume replica
* `CSI driver` runs on each node. Manage block device: format and mount to node
* Longhorn is managed via Kubernetes `CSI plugin` i.e.: Longhorn implements CSI standard. 
  > * `Kubelet` calls CSI drivers to mount/ unmount volume
  > * CSI driver watches Kubernetes API for triggering CIS operation like create, (node) attach, snapshot, ...
* Longhorn uses `iSCSI` for managing block storages

### Longhorn replica
* Each replica is a chain of snapshots. 
  > * The oldest snapshot is the base layer. 
  > * The newer snapshot is a layer on top of the older layer
  > * The newest data is in live data layer (top layer)
* `Read index` points which layer the latest 4K data block can be found
  > * `Read index` is kept in memory. 
    >> * Index pointer size is 1 byte -> Maximum 254 snapshots + 1 live data. 
    >> * 1 TB volume -> 256 MB for read index
  
* How new replica is created
  * Pause R&W operations
  * New blank replica is added in WO mode
  * Exisint replicas are snapshoted 
  * Unpause R&W operations
  * New data is write into a new layer for all replicas (inlcuding new replica)
  * Synchronize diff from old replicas -> new replica
  * Set the new replica to R&W mode

### Longhorn snapshot
* Snapshot is a layer of data
* When snapshot is created, it will not be changed. The exception is when the older snapshot is deleted, the data in the deleted snapshot is confliated into the newer one.
* Snapshot is incremental i.e.: only has overwriten data comparing to the previous snapshot
* Deleting a snapshot means that data in that snapshot conflated to the newer snapshot layer.

### Longhorn backup
* Backup = flattened version of snapshot chain
* Backup doesn't container snapshoting information
* A replica with 100 snapshots can have size of 100GB, but a backup can be 2MB only after flattening all snapshot layers.
* Backup is incremental.
  > * 1 MB Backup block = 500 4K data block. 
  > * When a 4K block change -> A new 1 MB block will be created
* Each backup is a `snapX.cfg` file, which contain the offents and checksums of all 2MB blocks in that backup.
* Each 2MB block is a `.blk` file

## Troubleshooting

### Volume in attach/ detach loop
1. Check instance-manager whether volume is in error state
2. Login to replica's node and verify data 
3. Check replica `volume.meta`, `volume-snap-*.img.meta` and `volume-head-XXX.img.meta` files for content

* Example `volume.meta` content
```
{"Size":8589934592,"Head":"volume-head-001.img","Dirty":true,"Rebuilding":false,"Error":"","Parent":"volume-snap-51131b80-b84f-4a33-abaf-7f8ea1a4468e.img","SectorSize":512,"BackingFilePath":""}
```
  > * Size = SizeInGiB x 1073741824
  > * Head = `volume-head-XXX.img` file 
  > * Parent = Latest `volume-snap-*.img.meta` in the directory 

* Example `volume-head-XXX.img.meta`
```
{"Name":"volume-head-001.img","Parent":"volume-snap-51131b80-b84f-4a33-abaf-7f8ea1a4468e.img","Removed":false,"UserCreated":false,"Created":"2021-07-25T23:44:51Z","Labels":null}
```
  > * Name = filename
  > * Parent = Latest `volume-snap-*.img.meta` in the directory 

* Example `volume-snap-XXX.img.meta`
```
{"Name":"volume-snap-51131b80-b84f-4a33-abaf-7f8ea1a4468e.img","Parent":"","Removed":true,"UserCreated":false,"Created":"2021-07-25T23:44:51Z","Labels":null}
```
  > * Name = filename 
  > * Parent = 2nd latest `volume-snap-*.img.meta` in the directory 