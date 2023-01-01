# Using Linode's CLI

Working with [Linode's CLI](https://www.linode.com/docs/products/tools/cli/get-started/)
is a timesaver when working with multiple servers and stores on Linode.

## Installation

The CLI is a Python project. To install:

```
pip install linode-cli
pip install boto  # if object store info is needed
```

Configure token and go.

## Usage

To get a list of all linodes:

```
linode-cli linodes list
```

The help information available from the command line is very good.

## Display output in different formats

There are a number of command line options to customize output for markdown,
json, and special formatting.

## Takeaway

Overall, the CLI is a timesaver over the GUI.
