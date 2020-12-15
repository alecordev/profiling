# Profiling

Profiling in Python.

Identify bottlenecks and measure execution times.

## Intro

The most common approach is to measure the time before and after an activity.

```python
import time
t0 = time.perf_counter()
activity_or_process()
time_taken = time.perf_counter() - t0
print(f'Total time taken was {time_taken}')
```

This can easily be put into a Python decorator for reuse and simplification.

## Using timeit

`python -m timeit '"-".join(map(str, range(100)))'`

or through code:

```python
import timeit
timeit.timeit('import time; time.sleep(2)', number=10000)
```

- https://docs.python.org/3.6/library/timeit.html

### Jupyter Notebooks

In a Jupyter Notebook, you can use the following to time the execution of a cell:

```python
%%timeit
np.random.randn(100000).cumsum()
```

## Using profile / cProfile

- https://docs.python.org/3.6/library/profile.html

## Dependencies

- gprof2dot
- graphviz

## Other modules for Profiling

- pyprof2calltree
- pyinstrument
- snakeviz

## Installing dependencies

As usual, `pip install <package>`.

Graphviz requires the graphviz binaries, usually in the PATH or available from the current working directory (http://www.graphviz.org/).

## Example 1

`$ python -m cProfile -s cumtime profile_me.py`

## Example 2

`$ python -m cProfile -o output.pstats profile_me.py`

`$ python -m gprof2dot -f pstats output.pstats >> stats.dot`

`$ dot -Tpng -o output.png stats.dot` - implies graphviz binaries are in the current directory or PATH.

## Using QCacheGrind

If you want to use QCacheGrindWin:

1) https://sourceforge.net/projects/qcachegrindwin/
2) Generate cProfile output
3) Use `pyprof2calltree` to convert the cProfile output to QCacheGrindWin file format

### Install The Convertor

`$ sudo pip install pyprof2calltree` - produces a file to be used with QCacheGrindWin and related applications.

### Profile The Python Code

`$ python -m cProfile -o <output_filename> filename_to_profile.py`

`$ pyprof2calltree -i output.pstats -o import.callgrind`

And open the `import.callgrind` with the QCacheGrindWin application.

## Using SnakeViz

`$ python -m cProfile -o program.prof my_program.py`

`$ snakeviz program.prof` - it will open a web application to view and analyze.

## Tools

- https://github.com/nvdv/vprof
- https://github.com/rkern/line_profiler

## Bibliography and Resources

- http://jiffyclub.github.io/snakeviz/
- https://github.com/jrfonseca/gprof2dot
- http://www.graphviz.org/doc/info/command.html
- https://julien.danjou.info/blog/2015/guide-to-python-profiling-cprofile-concrete-case-carbonara
