# SamTools service {#samtools_service}

The SamTools service allows the Grassroots Server to use the functionality provided by [Samtools](http://www.htslib.org) by Heng Li *et al.*. 
Currently it has the ability to retrieve a complete named scaffold from some sequence data.

## Installation

To build this service, you need the [grassroots core](https://github.com/TGAC/grassroots-core) and [grassroots build config](https://github.com/TGAC/grassroots-build-config) installed and configured. 

The files to build the SamTools service are in the ```build/<platform>``` directory. 

### Linux

Enter the build directory 

```
cd build/linux
```

and create a *user.prefs* file.

```
cp example-user.prefs user.prefs
```

You will need to edit this file to configure where the SamTools dependencies are stored. The file content is similar to the following

``` 
#
# samtools dependencies
#
# Set this to where you have the htslib directory 
# containing "include" and "lib" subdirectories.
export HTSLIB_HOME := $(DIR_GRASSROOTS_EXTRAS)/htslib
```

Adjust the ```HTSLIB_HOME``` to where you have htslib installed. You can then build the service by typing

```
make all
```

and then 

```
make install
```

to install the service into the Grassroots system where it will be available for use immediately.


## Configuration options

The service can be configured by a file with the same names in the ```config``` directory in the Grassroots application directory, *e.g.* ```config/SamTools service```. 


* **index_files**: This is an array of objects with each consisting of two key-value pairs.
 Either option is sufficient when attempting to run the SamTools service.
 
 * **Blast database**: The name of the Blast database file that SamTools can run against.
 * **Fasta**: The Fasta file that the Blast database was generated from.

 