

## Snapshotter
* Ref: https://github.com/kubernetes-csi/external-snapshotter/tree/master
* GA since 1.20
* Independent of any CSI driver 
* Components
  > * Snapshot controller
    >> * Watches VolumeSnapshot and VolumeSnapshotContent
  > * CSI Snapshotter sidecar
    >> * Watches VolumeSnapshotContent
    >> * Talks to CSI over socket (`/run/csi/socket` by default)