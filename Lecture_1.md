# Lecture 1

## Introduction
This is a course about infrastructure for applications.
  * Storage.
  * Communication.
  * Computation.

### Scalability:
* Horizontal scale: Increase number of devices
* Vertical scale: Increase resources of devices

### Fault tolerance:
* Availability
* Recoverability

### Consistency
Distributed storage of key value pairs.
Two operations allowed: GET, PUT.
Rules for replication are important as, access secondary only when primary fails etc.
	
## MapReduce:
1. Divide the input key value pairs into M splits
2. Call Map function on every input spit to generate o/p key-value pair.
3. Combine all the results from intermediate files by the use of Reducers.
Combine output from R reducers.

### Example
Word count
Input 1 -> Map a,1
Input 2 -> Map    b,1
Input 3 -> Map a,1   c,1

Reduce -> a,2
Reduce -> b,1
Reduce -> c,1

``` cpp
void Map(k,v) {
// k->filename, v->file contents
    Split_v_into_words(v);
    for(auto  word:words)
        emit(word,1);
}
```

``` cpp
void Reduce(k,v) {
//k-> word, v ->word
    emit(len(v));
}
```
GFS : Google File System
An optimization to avoid the unnecessary network file read, GFS and Mappers used to run on the same machine. So the controller used to try to run map jobs based on the server storing the input data.