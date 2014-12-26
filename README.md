rdocker
=======

# Usage : 
```
rdocker <remote> <command>
```

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
	Port 2376
	TLS yes
	TLSVerify yes
	TLSCACert <CA_CERT_FILE_PATH>
	TLSCert <CERT_FILE_PATH>
	TLSKey <KEY_FILE_PATH>
	
Remote container1.secured.remote
	Port 2376
	TLS yes
	TLSVerify yes
	TLSCACert <CA_CERT_FILE_PATH>
	TLSCert <CERT_FILE_PATH>
	TLSKey <KEY_FILE_PATH>
	DefaultCommand "exec -t -i container1 bash"

Remote unsecured.remote
	Port 2375

Remote bash.unsecured.remote
	DefaultCommand run -t -i ubuntu bash
	Host unsecured.remote
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
