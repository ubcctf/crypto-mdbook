# Assorted guides

Various guides for useful techniques when solving cryptography challenges


## z3

[Full guide](/assorted/z3.md)

`z3` is a useful tool for solving sets of constraints, for example when you know the state of the random number generator after n steps and want to easily recover the state from the start

## Rust

[Full guide](/assorted/rust.md)

`python` is very convinient for communicating with services and rapidly prototyping but is often too slow for anything beyond a quick bruteforce. `rust` is very very fast, supports very easy python interop using `pyo3`, and has easy multithreaded iteration using `rayon`. 