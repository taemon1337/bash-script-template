# bash-script-template
A simple bash script template for a CLI tool

### Example Usage
```
./run.sh help
./run.sh <action> <options>

This is an example of a bash cli tool help and usage

Actions:
  help                                          show this help menu
Options:
  -v|--verbose|--debug                          print debug statements
  
```

### Bash scripting with command line argument parsing
```
#!/bin/bash
OWD=$(pwd)
DIR="$( cd "$( dirname "${BASH_SOURCE[0]}" )" && pwd )"
cd $DIR

_help() {
  echo "$0 <action> <options>"
  echo "This is an example of a bash cli tool help and usage"
  echo ""
  echo "Actions:"
  echo "  help                                          show this help menu"
  echo "Options:"
  echo "  -v|--verbose|--debug                          print debug statements"
  echo ""
}

_debug() {
  if [ -n "$DEBUG" ]; then echo $1; fi
}

_main() {
  case "$1" in
    help)
      shift
      _help "${@}";;
    *)
      _help;;
  esac
}

# Default variables
DEBUG=""

# parse args
args=()
while [[ $# -gt 0 ]]; do
  key="$1"
  case $key in
    -v|--verbose|--debug)
      DEBUG="1"
      shift
      ;;
    *)
      args+=("$1")
      shift
      ;;
  esac
done

_main "${args[@]}"
cd $OWD
```
