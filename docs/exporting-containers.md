# Exporting Containers
To Export your containers, and want to experiment with your container and save your current state

The `rlc-export` command allows you to export your entire container installation, before you back up your containers, you should close all the running containers.

Example:
```
rlc-export mycontainer
```

This will dump the container into gzipped tarball (stdout export isn't yet implemented)

***Notes when backing up containers***
* The exported container will be outputed at `$HOME/exported_containers`
* Data corruption may occur when running containers during the export process
* This will output the tarball into gzip

# Importing the container
Sometimes it's useful to rollback the state where you're working on

To import the containers, use `rlc-import` command

Example:
```
rlc-import container.tar.gz
```

This will delete existing files and overwrites them with previous state of files
