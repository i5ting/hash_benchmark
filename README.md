# Benchmarking MRI’s hash implementation

The point of this experiment is to benchmark MRI's hash table implementation vs others to see if it can be improved upon.

Right now there are three contenders:

- st (not the modified one bundled with Ruby, as I wasn't able to get it to work yet.)
- uthash (can be found [here](https://github.com/troydhanson/uthash))
- tommy hash (can be found [here](http://tommyds.sourceforge.net))
- khash (can be found [here](https://github.com/attractivechaos/klib/blob/master/khash.h))

Code is compiled with `-O3` and binds to `jemalloc`

## Results

__This is very incomplete, more to come.__

All these tests are run with:
- 2 runs
- 100,000 iterations each
- 100 different keys on each iteration

Results are ordered from fastest to slowest.

### Writes

```
uthash:           126232.98 i/sec (1.584372 seconds)
tommy (dyn hash): 117290.91 i/sec (1.705162 seconds)
tommy (lin hash): 107630.76 i/sec (1.858205 seconds)
khash:            80183.53 i/sec  (2.494278 seconds)
st:               60721.43 i/sec  (3.293730 seconds)
```

### Reads

```
tommy (dyn hash): 938341.94 i/sec (0.213142 seconds)
khash:            678108.42 i/sec (0.294938 seconds)
tommy (lin hash): 598229.12 i/sec (0.334320 seconds)
st:               416710.12 i/sec (0.479950 seconds)
uthash:           261664.34 i/sec (0.764338 seconds)
```

### Random reads

```
tommy (dyn hash): 456022.31 i/sec (0.438575 seconds)
khash:            378375.18 i/sec (0.528576 seconds)
tommy (lin hash): 300879.51 i/sec (0.664718 seconds)
st:               207201.69 i/sec (0.965243 seconds)
uthash:           187864.16 i/sec (1.064599 seconds)
```

### Non-existant key reads

```
tommy (dyn hash): 941362.99 i/sec (0.212458 seconds)
tommy (lin hash): 566448.78 i/sec (0.353077 seconds)
khash:            495424.86 i/sec (0.403694 seconds)
st:               345405.22 i/sec (0.579030 seconds)
uthash:           334257.56 i/sec (0.598341 seconds)
```

### Write & Delete (same key)

```
tommy (dyn hash): 31298440.41 i/sec (0.006390 seconds)
khash:            30487399.60 i/sec (0.006560 seconds)
tommy (lin hash): 29343109.00 i/sec (0.006816 seconds)
st:               7105316.74 i/sec  (0.028148 seconds)
uthash:           5189011.57 i/sec  (0.038543 seconds)
```
