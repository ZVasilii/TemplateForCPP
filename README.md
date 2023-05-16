# Template

Template for C++ projetcs with build system and GTest

## Usage

```
cd build/
cmake -DCMAKE_BUILD_TYPE=<type> ..
make -j<number_of_workers>
ctest -VV
