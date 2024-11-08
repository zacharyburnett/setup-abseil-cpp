# setup-abseil-cpp
### action to build and install [`abseil/abseil-cpp`](https://github.com/abseil/abseil-cpp) within a GitHub Workflow runner

## Example

```yaml
jobs:
  build-with-abseil:
    strategy:
      matrix:
        runs-on:
          - ubuntu-latest
          # macos-13 is an intel runner, macos-14 is apple silicon
          - macos-13
          - macos-latest
      fail-fast: false
    runs-on: ${{ matrix.runs-on }}
    steps:
      - uses: zacharyburnett/setup-abseil-cpp@cb29bd8e459ccdabb0f7280ccdd3885479e4cf01 # 1.0.1
        with:
          cmake-build-args: "-DCMAKE_CXX_STANDARD=17 -DABSL_PROPAGATE_CXX_STD=ON -DABSL_ENABLE_INSTALL=ON -DBUILD_TESTING=off -DCMAKE_POSITION_INDEPENDENT_CODE=ON"
          abseil-version: "20240722.0"
      - uses: actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4.2.2
      - run: mkdir build
      - run: cmake -DCMAKE_CXX_STANDARD=17 -DCMAKE_PREFIX_PATH=/usr/local/lib/ -DBUILD_TESTS=OFF ..
        working-directory: build/
      - run: make -j $(nproc)
        working-directory: build/
      - run: sudo make install
        working-directory: build/
```

## Inputs

```yaml
inputs:
  cmake-build-args:
    description: "arguments to pass to CMake"
    required: false
    default: "-DCMAKE_CXX_STANDARD=17 -DABSL_PROPAGATE_CXX_STD=ON -DABSL_ENABLE_INSTALL=ON -DBUILD_TESTING=off"
  cmake-version:
    description: "version of CMake to use"
    required: false
    default: ""
  abseil-version:
    description: "tag or ref of `abseil/abseil-cpp`"
    required: false
    default: "20240722.0"
```
