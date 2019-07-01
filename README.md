# kubectl-ikc

Simple CLI tool (Python script) to import context from one `kubectl` config to another.

Requires `python` to be installed (which is by default on many un*x systems). Uses only standard libraries so it should work fine on most distros.

## Usage

```
usage: kubectl-ikc [-h] [-s SRC_FILENAME] [-d DST_FILENAME] [-o OUT_FILENAME]
                   [--backup BACKUP_FILENAME] [--prefix PREFIX] [--use]
                   src_context [dst_context]

Import kubectl config context from one config to another.

positional arguments:
  src_context           Source context name
  dst_context           Destination context name (new one), defaults to source
                        context name

optional arguments:
  -h, --help            show this help message and exit
  -s SRC_FILENAME       Source config filename (or "-" for stdin), defaults
                        to: -
  -d DST_FILENAME       Destination config filename, defaults to:
                        ~/.kube/config
  -o OUT_FILENAME       Output config filename (or "-" for stdout), defaults
                        to destination config
  --backup BACKUP_FILENAME
                        Destination config backup filename, defaults to output
                        config + ".backup"
  --prefix PREFIX       Cluster and user prefix (defaults to source context)
  --use                 Activates destination context
```

## Examples

```bash
# Import remote context to local kubectl config
ssh user@server "cat ~/.kube/config" | ./kubectl-ikc remote_cluster local_cluster

# Import context from source file to local kubectl config
./kubectl-ikc -s ./local_config minikube minikube_new

# Import context from source file and write output to stdout
./kubectl-ikc -s ./local_config -o - minikube minikube_new

# Import context from source file and write output to another file
./kubectl-ikc -s ./local_config -o ./new_config minikube minikube_new

# Import context from source file, add it to destination file and write output to another file
./kubectl-ikc -s ./remote_config -d ./local_config -o ./new_config minikube minikube_new

# Import context from source file to local file and activate new context
./kubectl-ikc -s ./local_config --use minikube minikube_new

# Improt context from source file, write output to stdout and change resource prefixes
./kubectl-ikc -s ./local_config -o - --prefix "my-server-" my.server remote_cluster
```

## Quick Install

```bash
# Download to local directory
wget -O ./kubectl-ikc https://raw.githubusercontent.com/jirihybek/kubectl-import-kubeconfig/master/kubectl-ikc && chmod +x ./kubectl-ikc

# Install to /usr/local/bin
wget -O /usr/local/bin/kubectl-ikc https://raw.githubusercontent.com/jirihybek/kubectl-import-kubeconfig/master/kubectl-ikc && chmod +x /usr/local/bin/kubectl-ikc
```

## License

The MIT License (MIT)

Copyright (c) 2019 Jiri Hybek jiri@hybek.cz (jiri.hybek.cz)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.