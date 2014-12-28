rdocker
=======

RDocker allow docker facility around remote api. It allow execute remote command on docker server without repeat common options.

# Usage : 
```
rdocker <remote> <command>
```

RDocker use local docker client. Local available commands may not be the same as remote command if remote version is lower than local version. Behavior may be also different accordian to differents version.

# Installation

clone project : 
```
git clone https://github.com/arcamael/rdocker <project_dir>
```

RDocker use "native" docker autocompletion added to its own remote completion. Source file <project_dir>/bash_completion/completion to enable RDocker completion on bash shell

$HOME/.bashrc example : 

```
# RDocker
source <rdocker_path>/bash_completion/completion
export PATH=$PATH:<rdocker_path>/scripts
```

# Configuration

RDocker use Remote host file (inspired from ssh client behavior)

Remote file example : 

```
Remote secured.remote
	Port 2376 # Configure remote port
	TLS yes # Enable --tls option
	TLSVerify yes # Enable --tlsverify option
	TLSCACert <CA_CERT_FILE_PATH> # Add --tlscacert option
	TLSCert <CERT_FILE_PATH> # Add --tlscert option
	TLSKey <KEY_FILE_PATH> # Add --tlskey option
	
Remote container1.secured.remote
	Port 2376
	TLS yes
	TLSVerify yes
	TLSCACert <CA_CERT_FILE_PATH>
	TLSCert <CERT_FILE_PATH>
	TLSKey <KEY_FILE_PATH>
	DefaultCommand "exec -t -i container1 bash" # Add a command to this remote, will be automatically called if not specified on the command line

Remote unsecured.remote
	Port 2375

Remote bash.unsecured.remote
	DefaultCommand run -t -i ubuntu bash
	Host unsecured.remote # Specify an alternative hostname
```

Usage example : 
* See remote version
```
rdocker unsecured.remote version
```
* Start a shell
```
rdocker bash.unsecured.remote
```
* Start a shell over secured connection
```
rdocker secured.remote run -t -i ubuntu bash
```
* Enter a docker container over a secured connection
```
rdocker container1.secured.remote
```

# Evolution : 

I'm not a bash killer, any PR are welcome
