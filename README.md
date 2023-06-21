# Template

Template for C++ projetcs with build system and GTest

@Vasilii, 2023
## Usage

```
cd build/
cmake -DCMAKE_BUILD_TYPE=<type> <other flags> ..
make -j<number_of_workers>
ctest -VV
```

## CMAKE Flags

*BUILD_TESTS* - Build Unit Tests \
*BUILD_DOC* - Make Doxygen TeX documentation \
*CMAKE_BUILD_TYPE* - Release/Debug build


## Documentation

Available [here](docs/documentation.pdf)
