# Using Linode object store like S3

## Using boto3 library with linode

This basic program sets the `boto3` config for Linode by mapping to the AWS variables. After that step, things work the same way as in S3.

Here's a sample program that lists buckets and their contents when environment variables are stored in `.env`.

```python
import os

import boto3
from dotenv import load_dotenv


load_dotenv()

# Create the config dictionary for boto3
config = {
    "aws_access_key_id": os.environ['LINODE_BUCKET_ACCESS_KEY'],
    "aws_secret_access_key": os.environ['LINODE_BUCKET_SECRET_KEY'],
    "endpoint_url": os.getenv('CLUSTER_URL'),
}

# Create query client
client = boto3.client('s3', **config)

# List buckets and contents
response = client.list_buckets()
for bucket in response['Buckets']:
    print(f"{bucket['Name']}: ")
    
    response = client.list_objects(Bucket=bucket['Name'])
    for object in response['Contents']:
        print(f"  {object['Key']}")
```

## linode-cli

An alternative would be to use the `linode-cli`.

```bash
λ › linode-cli                                                                                                               sandbox/botolinode
usage: linode-cli [--help] [--text] [--delimiter DELIMITER] [--json] [--markdown] [--pretty] [--no-headers] [--page PAGE]
                  [--page-size PAGESIZE] [--all] [--format FORMAT] [--no-defaults] [--as-user USERNAME] [--suppress-warnings] [--version]
                  [--debug]
                  [COMMAND] [ACTION]

positional arguments:
  COMMAND               The command to invoke in the CLI.
  ACTION                The action to perform in this command.

optional arguments:
  --help                Display information about a command, action, or the CLI overall.
  --text                Display text output with a delimiter (defaults to tabs).
  --delimiter DELIMITER
                        The delimiter when displaying raw output.
  --json                Display output as JSON
  --markdown            Display output in Markdown format.
  --pretty              If set, pretty-print JSON output
  --no-headers          If set, does not display headers in output.
  --page PAGE           For listing actions, specifies the page to request
  --page-size PAGESIZE  For listing actions, specifies the number of items per page, accepts any value between 25 and 500
  --all                 If set, displays all possible columns instead of the default columns. This may not work well on some terminals.
  --format FORMAT       The columns to display in output. Provide a comma-separated list of column names.
  --no-defaults         Suppress default values for arguments. Default values are configured on initial setup or with linode-cli configure
  --as-user USERNAME    The username to execute this command as. This user must be configured.
  --suppress-warnings   Suppress warnings that are intended for human users. This is useful for scripting the CLI's behavior.
  --version, -v         Prints version information and exits.
  --debug               Enable verbose HTTP debug output

CLI user management commands:
┌─────────────┬──────────┬────────────┐
│ configure   │ set-user │ show-users │
│ remove-user │          │            │
└─────────────┴──────────┴────────────┘

CLI Plugin management commands:
┌─────────────────┬───────────────┐
│ register-plugin │ remove-plugin │
└─────────────────┴───────────────┘

Other CLI commands:
┌────────────┐
│ completion │
└────────────┘

Available commands:
┌────────────────────┬───────────────────┬─────────────────┐
│ account            │ databases         │ domains         │
│ events             │ firewalls         │ images          │
│ kernels            │ linodes           │ lke             │
│ longview           │ managed           │ networking      │
│ nodebalancers      │ object-storage    │ payment-methods │
│ phone              │ profile           │ regions         │
│ security-questions │ service-transfers │ sshkeys         │
│ stackscripts       │ tags              │ tickets         │
│ users              │ vlans             │ volumes         │
└────────────────────┴───────────────────┴─────────────────┘
Available plugins:
┌─────────────────┬──────────────┬─────┐
│ firewall-editor │ image-upload │ obj │
│ ssh             │              │     │

```

## Notes

You may need to set ACL for the bucket itself through the Linode GUI interface.
