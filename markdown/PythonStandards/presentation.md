# Python Packages for Science


Ricardo M. Ferraz Leal

[rhf@ornl.gov](mailto:rhf@ornl.gov?subject=CleanCodeIn5Minutes)

---

# Standard Data formats

- Pandas Dataframes
  - New: Release the Global Interpreter Lock (GIL) on some cython operations!
- Numpy Arrays
  - numpy code often releases the GIL while it is calculating.

---

# Dask:

- Parallel computing: threading, multiprocessing, etc.. (no need for launching mpi clusters)
- Talk from SciPy: https://speakerdeck.com/jcrist/pandas-through-task-scheduling

  - dask.array = numpy + threading
  - dask.dataframe = pandas + threading  
  - dask.bag = map, filter, itertools, toolz + multiprocessing

Dask releasing the GIL with Numba:
http://dask.readthedocs.org/en/latest/array-api.html#dask.array.core.Array.map_blocks

Dask.array: Calculations with arrays bigger than your memory:
http://earthpy.org/dask.html

Video:
https://www.youtube.com/watch?v=HLME2WKTJJ8

https://github.com/ContinuumIO/dask

http://dask.pydata.org/

---

# Xray

- Extension to pandas for labeled multi-dimensional arrays.
- Parallel processing
- Notebook [here](http://nbviewer.ipython.org/urls/gist.githubusercontent.com/shoyer/be3749849809fe35efa8/raw/d3ac4af07343391ef005d2dbea80368efc9ee1f6/xray-demo-python-workers-party.ipynb).

https://github.com/xray/xray

http://xray.readthedocs.org

---

# Xray + Dask:

Xray provides labeled, multi-dimensional arrays. Dask provides a system for parallel computing. Together, they allow for easy analysis of scientific datasets that don’t fit into memory.

Example:
https://www.continuum.io/content/xray-dask-out-core-labeled-arrays-python

---

# DistArray

The Distributed Array Protocol (DAP) is a process-local protocol that allows two subscribers, called the producer and the consumer or the exporter and the importer, to communicate the essential data and metadata necessary to share a distributed-memory array between them.

- Needs IPython da cluster running: ```dacluster start -n4```
- Notebook: https://github.com/enthought/distarray/blob/master/examples/features.ipynb

https://github.com/enthought/distarray

http://docs.enthought.com/distarray/

---

# Cython

- Can invoke C/C++ routines
- Declares static type of subroutine parameters and results, local variables, and class attributes.
- I.e. Python to C source code translator that integrates with the CPython interpreter on a low level.

http://cython.org/

http://docs.cython.org/

---

# Numba

- Numba works by generating optimized machine code using the LLVM compiler infrastructure.
```python
# jit decorator tells Numba to compile this function.
# The argument types will be inferred by Numba when function is called.
@jit
def sum2d(arr):
```
- A function can be compiled into a Numpy ufunc using:
```python
@vectorize([float64(float64, float64)])
def f(x, y):
    return x + y
```

https://github.com/numba/numba

http://numba.pydata.org/

---

# ODO

To convert file format:
https://odo.readthedocs.org/en/latest/

---

# Blaze

For everything:
http://blaze.pydata.org/
