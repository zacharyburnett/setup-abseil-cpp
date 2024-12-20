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
      - uses: zacharyburnett/setup-abseil-cpp@41fabae9b8c6a76c1b9612c8611c50b498bbeda1 # 1.0.3
        with:
          cmake-build-args: "-DCMAKE_CXX_STANDARD=17 -DABSL_PROPAGATE_CXX_STD=ON -DABSL_ENABLE_INSTALL=ON -DBUILD_TESTING=off -DCMAKE_POSITION_INDEPENDENT_CODE=ON"
          abseil-version: "20240722.0"
      - uses: actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4.2.2
      - run: mkdir build
      - run: cmake ..
        working-directory: build/
      - run: sudo cmake --build . --parallel=2
        working-directory: build/
```

## Inputs

|                    |         `description`             | `required` | `default` |
| ------------------ | --------------------------------- | ---------- | --------- |
| `cmake-build-args` | arguments to pass to CMake        |  `false`   | `"-DCMAKE_CXX_STANDARD=17 -DABSL_PROPAGATE_CXX_STD=ON -DABSL_ENABLE_INSTALL=ON -DBUILD_TESTING=off"` |
| `cmake-version `   | version of CMake to use           |  `false`   | `""` |
| `abseil-version`   | tag or ref of `abseil/abseil-cpp` |  `false`   | `"20240722.0"` |
