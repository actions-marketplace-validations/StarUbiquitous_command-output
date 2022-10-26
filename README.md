# Command Output Action

[![Continuous Integration](https://github.com/StarUbiquitous/command-output/actions/workflows/continuous-integration.yml/badge.svg)](https://github.com/StarUbiquitous/command-output/actions/workflows/continuous-integration.yml)
[![CodeQL](https://github.com/StarUbiquitous/command-output/actions/workflows/codeql-analysis.yml/badge.svg)](https://github.com/StarUbiquitous/command-output/actions/workflows/codeql-analysis.yml)

A `run` alternative that stores command output in a variable.

## Inputs

### `run`

**Required** The command to run.

### `shell`

The shell used to run command.

## Outputs

### `stdout`

The output of the command written to stdout.

### `stderr`

The output of the command written to stderr.

## Example usage

#### Store today's date in variable

```yaml
steps:
- name: Get today's date
  uses: StarUbiquitous/command-output@v1.0.0
  id: today
  with:
    run: date +'%Y-%m-%d'

- run: echo Today is ${{ steps.today.outputs.stdout }}
```

#### Use stdout and stderr output as condition

```yaml
steps:
- name: Read file if it exists?
  uses: StarUbiquitous/command-output@v1.0.0
  continue-on-error: true
  id: cmd
  with:
    run: cat unknown.txt

- run: echo Command succeeded
  if: ${{ steps.cmd.outputs.stdout }}

- run: echo Command failed
  if: ${{ steps.cmd.outputs.stderr }}
```


