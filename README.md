# Rackspace Cloud Queues API documentation

[![Build Status](https://travis-ci.org/rackerlabs/docs-cloud-queues.svg?branch=master)](https://travis-ci.org/rackerlabs/docs-cloud-queues)


## Purpose

This GitHub repository contains the source files for the following Rackspace Cloud Queues API documentation:

* [Cloud Queues Developer Guide](https://developer.rackspace.com/docs/cloud-queues/v1/developer-guide/)

## Contributing

Contributions are welcome! 

* To suggest changes or report a problem, submit an [issue](https://github.com/rackerlabs/docs-cloud-queues/issues). 

* To make changes to a project, create your own fork of the repository. Then, submit a [pull 
request](https://github.com/rackerlabs/docs-cloud-queues/compare?expand=1) to have your changes reviewed 
and merged into the master branch as appropriate.

To contribute content, all you need is an editor and a 
basic understanding of the project layout and [reStructuredText](http://sphinx-doc.org/rest.html) syntax.

You can use the GitHub editor or any text editor to work with documentation source files. For quick syntax checking, try the 
[Online restructuredText editor](http://rst.ninjs.org/). 

**Note:** If you want to build the project, you need to install the [Sphinx documentation generator](http://www.sphinx-doc.org/en/stable/install.html). 

## Source format

The Rackspace developer documentation is developed and built using the [Python Sphinx documentation generator](http://sphinx-doc.org/). Content is 
written in [reStructuredText](http://sphinx-doc.org/rest.html), the markup syntax and parser component of 
[Python Docutils](http://docutils.sourceforge.net/index.html).

The repository includes the documentation source files, 
Sphinx configuration and build files, as well any required Sphinx 
extensions and build tools. 

## Structure

Source files for the Sphinx documentation project are in the ``api-docs`` directory. Here are the key files that define 
the Sphinx project and content architecture for the documentation: 

* [conf.py](https://github.com/rackerlabs/docs-cloud-queues/blob/master/api-docs/conf.py): Sphinx documentation configuration file. (Typically, this file does not require changes.)
* [index.rst](https://github.com/rackerlabs/docs-cloud-queues/blob/master/api-docs/index.rst): Index page for the main content structure.
* [overview/index.rst](https://github.com/rackerlabs/docs-cloud-queues/blob/master/api-docs/overview/index.rst): Index for the Overview section.
* [getting-started.rst](https://github.com/rackerlabs/docs-cloud-queues/blob/master/api-docs/getting-started.rst): Introduction to the Getting Started section. 
* [getting-started/index.rst](https://github.com/rackerlabs/docs-cloud-queues/blob/master/api-docs/getting-started/index.rst): Top-level index for the Getting Started section.
* [developer-guide.rst](https://github.com/rackerlabs/docs-cloud-queues/blob/master/api-docs/developer-guide.rst): Introduction to Developer Guide
* [general-api-info/index.rst](https://github.com/rackerlabs/docs-cloud-queues/blob/master/api-docs/general-api-info/index.rst): Top-level topic index for the General API Information section.
* [api-reference.rst](https://github.com/rackerlabs/docs-cloud-identity/blob/master/api-docs/api-reference.rst): Introduction to API reference.
* [api-operations/index.rst](https://github.com/rackerlabs/docs-cloud-queues/blob/master/api-docs/api-operations/index.rst): Index for API Reference.
* [api-operations/methods](https://github.com/rackerlabs/docs-cloud-queues/tree/master/api-docs/api-operations/methods): 
Individual files for each API operations method, including code samples (converted from WADL).
* **make.bat**: Windows build script
* **Makefile**: Linux and OS X build

### Support and feedback

If you find a problem, open a GitHub [issue](https://github.com/rackerlabs/docs-cloud-identity/issues).

If you need additional assistance, contact us at [devdoc@rackspace.com](mailto:devdoc@rackspace.com).
