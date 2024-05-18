
## Single index
| Search key | Data reference/ Data pointer | 
| --- | --- |


### Dense index 

* Index record that containes search key and pointer for every search key in the data set

* Benefit
  > * Cover all search values for data set

* Limitation
  > * Index record size

### Sparse index

* Index record only includes search key and pointer for part of the data set

* Benefit
  > * Storage efficiency

* Limitation
  > * Missing records, which are not indexed, are slow