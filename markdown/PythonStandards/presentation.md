# Python Packages for Science


Ricardo M. Ferraz Leal

[rhf@ornl.gov](mailto:rhf@ornl.gov?subject=CleanCodeIn5Minutes)

---

# Standard Data formats

- [Pandas](http://pandas.pydata.org/) Dataframes
  - Tabular data.
  - `Panel`: 3-dimensional array:
    * `labels`, `major_axis`, `minor_axis`
  - `Panel4D` (Experimental)
    * `labels`, `items`, `major_axis`, `minor_axis`
  - Lots of functionality: statistics, interpolation, mask, etc  
  - New: Release the Global Interpreter Lock (GIL) on some `cython` operations!
- Numpy Arrays
  - numpy code often releases the GIL while it is calculating.

---

# New Standards

---

# [xarray](http://xarray.pydata.org/) (formerly xray):

- Extension to pandas for labeled multi-dimensional arrays.
- Xray uses NetCDF4 (hence HDF5) for persistent storage.

References:
- Notebook [here](http://nbviewer.ipython.org/urls/gist.githubusercontent.com/shoyer/be3749849809fe35efa8/raw/d3ac4af07343391ef005d2dbea80368efc9ee1f6/xray-demo-python-workers-party.ipynb).
- Presentation of Xray at SciPy 2015 [here](http://www.slideshare.net/stephanhoyer/xray-nd-labeled-arrays-and-datasets-in-python).

---

# [Dask](http://dask.pydata.org/):

- Parallel computing: threading, multiprocessing, etc..
  - dask.array = numpy + threading
  - dask.dataframe = pandas + threading  
  - dask.bag = map, filter, itertools, toolz + multiprocessing

My test [here](https://github.com/ricleal/PythonParallel/blob/master/Dask/Dask%20arrays%201.ipynb)

References:
- Talk from SciPy [here](https://speakerdeck.com/jcrist/pandas-through-task-scheduling).
- Dask releasing the GIL with Numba [here](http://dask.readthedocs.org/en/latest/array-api.html#dask.array.core.Array.map_blocks).
- Dask.array: Calculations with arrays bigger than your memory
[here](http://earthpy.org/dask.html).
- [Article](http://conference.scipy.org/proceedings/scipy2015/pdfs/matthew_rocklin.pdf).

---


# Xray + Dask:

- Xray provides labeled, multi-dimensional arrays.
- Dask provides a system for parallel computing.
- Together, they allow for easy analysis of scientific datasets that don’t fit into memory.

References:
- Example [here](https://www.continuum.io/content/xray-dask-out-core-labeled-arrays-python)

---

# [DistArray](http://docs.enthought.com/distarray/)

The Distributed Array Protocol (DAP) is a process-local protocol that allows two subscribers, called the producer and the consumer or the exporter and the importer, to communicate the essential data and metadata necessary to share a distributed-memory array between them.

- Enthought version of Dask (?)
- Needs IPython da cluster running: ```dacluster start -n4```
- Notebook [here](https://github.com/enthought/distarray/blob/master/examples/features.ipynb)

---

# [Cython](http://cython.org/)

Python with types...

- Can invoke C/C++ routines
- Declares static type of subroutine parameters and results, local variables, and class attributes.
- I.e. Python to C source code translator that integrates with the CPython interpreter on a low level.
- My tests [here](https://github.com/ricleal/PythonParallel/tree/master/Cython).

---

# [Numba](http://numba.pydata.org/)

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

---

# [ODO](https://github.com/blaze/odo)

To convert file/data formats

![](https://raw.githubusercontent.com/blaze/odo/master/docs/source/images/conversions.png)

---

# [Blaze](http://blaze.pydata.org/)

The Blaze ecosystem is a set of libraries that help users store, describe, query and process data. It is composed of the following core projects:

* Blaze: An interface to query data on different storage systems
* Dask: Parallel computing through task scheduling and blocked algorithms
* Datashape: A data description language
* DyND: A C++ library for dynamic, multidimensional arrays
* Odo: Data migration between different storage systems

---

# [Seaborn](http://stanford.edu/~mwaskom/software/seaborn/#): statistical data visualization

```
import seaborn as sns
sns.jointplot(data=df, kind="kde");
```

![](http://stanford.edu/~mwaskom/software/seaborn/_images/distributions_34_0.png)
---



---

Our `Workspace2D` could be exported to a Pandas Dataframe

pixel_id, x, y, z, panel_id, panel_x, panel_y, times[n]/bins[n]
