# Add-Identifier
This is a GitHub Action to add identifier for filename of artifacts

[![workflow](https://github.com/elehobica/add-identifier/actions/workflows/test1.yml/badge.svg)](https://github.com/elehobica/add-identifier/actions/workflows/test1.yml)

## Overview
* Change filename of artifacts by adding identifier
* Change filename of artifacts by adding run-number (with offset)

## Usage
* To use this GitHub Action in your workflow, add the following step to your `.github/workflows/your-workflow.yml` file.
* It is supposed to use this GitHub Action in between when artifacts are generated and when the artifacts are uploaded.

```yaml
name: Add-Identifier example

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      ...
      - name: add-identifier
        uses: elehobica/add-identifier@v1
        with:
          paths: ./build
          exts: .elf .uf2
          identifier: pico
          run_number_offset: 100
      ...
```

If following files are given for the branch _test-branch_ and run-number _25_:
* `build/project.elf`
* `build/project.uf2`

The result after applying above GitHub Action will be:
* `build/project-pico-test-branch-125.elf`
* `build/project-pico-test-branch-125.uf2`

If same condidtion is given except for the tag _1.0.0_ not the branch, the result will be:
* `build/project-pico-1.0.0.elf`
* `build/project-pico-1.0.0.uf2`

## Inputs
| Inputs | Description | Default | Required |
----|----|----|----
| paths | Path(s) from working directory. Multiple designations possible by separating with ' ' | ./build | true |
| exts | Ext(s) for the files to add identifier. Multiple designations possible by separating with ' ' | .bin .hex | true |
| identifier | Identifier to add | identifier | true |
| run_number_offset | Offset for run-number | 0 | false |
| omit_run_number_for_tag | Omit run-number for _tag_ target (true or false) | true | false |

## Sample script
See [test1.yml](.github/workflows/test1.yml)