# HdfsBrowser

Hadoop JupyterLab Extension

This extension is composed of a Python package named `hdfsbrowser`, which installs the server+nbextension and a NPM package named `@swan-cern/hdfsbrowser`
for the JupyterLab extension.

![Hadoop JupyterLab Extension](hdfsbrowser.png)

## Requirements

* JupyterLab >= 2.1
* NodeJs >= 10

## Install

Note: You will need NodeJS to install the extension.
Can be installed with
```bash
curl -sL https://rpm.nodesource.com/setup_10.x | sudo bash -
```

```bash
pip install hdfsbrowser
jupyter nbextension install hdfsbrowser --py
jupyter nbextension enable  hdfsbrowser --py
jupyter lab build
```

## Configure extension to work with Hadoop cluster through hdfs-site.xml

Configure notebook `jupyter_notebook_config.py`:

```
# Location of the hdfs-site.xml file
c.HDFSBrowserConfig.hdfs_site_path = "/etc/hadoop/conf/hdfs-site.xml"

#This property in hdfs-site.xml will be used to find the hostnames of the namenodes
# If you have the namenode IDs be different from their hostnames, you must create a new property with the hostnames
c.HDFSBrowserConfig.hdfs_site_namenodes_property = "dfs.ha.namenodes.analytix"

c.HDFSBrowserConfig.hdfs_site_namenodes_port = "50070"

# Can be created with hdfs fetchdt --renewer "dummy" tokenfile, I think
c.HDFSBrowserConfig.webhdfs_token = "dummy"
```

This can be located in `~/.jupyter/jupyter_notebook_config.py`


## Troubleshoot

If you are not seeing the frontend, check if it's installed:

```bash
jupyter labextension list
```

If it is installed, try:

```bash
jupyter lab clean
jupyter lab build
```

## Contributing

### Install

The `jlpm` command is JupyterLab's pinned version of
[yarn](https://yarnpkg.com/) that is installed with JupyterLab. You may use
`yarn` or `npm` in lieu of `jlpm` below.

```bash
# Clone the repo to your local environment
# Move to hdfsbrowser directory

# Install server extension
# This will also build the js code
pip install -e .

# Install and enable the nbextension
jupyter nbextension install hdfsbrowser --py --sys-prefix
jupyter nbextension enable  hdfsbrowser --py --sys-prefix

# Link your development version of the extension with JupyterLab
jupyter labextension link .
# Rebuild JupyterLab after making any changes
jupyter lab build

# Rebuild Typescript source after making changes
jlpm build
# Rebuild JupyterLab after making any changes
jupyter lab build
```

You can watch the source directory and run JupyterLab in watch mode to watch for changes in the extension's source and automatically rebuild the extension and application.

```bash
# Watch the source directory in another terminal tab
jlpm watch
# Run jupyterlab in watch mode in one terminal tab
jupyter lab --watch
```

### Uninstall

```bash
pip uninstall hdfsbrowser
jupyter labextension uninstall @swan-cern/hdfsbrowser
# Rebuild JupyterLab after making any changes
jupyter lab build
```
