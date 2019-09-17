# CentOS 8 Documentation

This repository contains sources that comprise the CentOS 8 documentation published on https://docs.centos.org/en-US/docs/.
Please report Issues and submit Pull Requests for **Content Fixes** here. For other issues or fixes, use:

* [CentOS_Docs](https://github.com/CentOS/docs) - the builder repository for the entire website, including for example structure configuration
* [CentOS_Docs_Web_UI](https://github.com/CentOS/docs-web-ui) - the website's user interface (e.g. CSS styling) sources

## Repository structure

The documentation is broken into four modules, placed in the `modules` directory.
Three of them correspond to separate "titles":

* `standard-install` - Performing a standard CentOS 8 installation - covers mostly installation using Anaconda's GUI
* `advanced-install` - Performing an advanced CentOS 8 installation - covers advanced install topics like Kickstart, remote access during installation, and PXE boot
* `managing-userspace-components` - Installing, managing, and removing user space components - information about modules and streams

Each of these modules contains sources which are rendered as separate pages. However, those sources use `include::` statements to include so-called "partials" - smaller bits of content that are not rendered separately. These partials, as well as global attributes used throughout this set of docs and the splash page, are stored in the `ROOT` module.

## Structure

```
|-- README.md
|-- antora.yml ....................... 1.
|-- build.sh ......................... 2.
|-- preview.sh ....................... 3.
|-- site.yml ......................... 4.
`-- modules
    `-- ROOT ......................... 5.
        |-- assets
        |   `-- images ............... 6.
        |       `-- pizza.png
        |-- nav.adoc ................. 7.
        `-- pages .................... 8.
            |-- architecture.adoc
            |-- community.adoc
            |-- faq.adoc
            |-- index.adoc
            |-- pizza-dough.adoc
            `-- pizza-owen.adoc
```

1. Metadata definition.
2. A script that does a local build. Uses docker.
3. A script that shows a preview of the site in a web browser by running a local web server. Uses docker.
4. A definition file for the build script.
5. A "root module of this documentation component". Please read below for an explanation.
6. **Images** to be used on any page.
7. **Menu definition.** Also defines the hierarchy of all the pages.
8. **Pages with the actual content.** They can be also organised into subdirectories if desired.

## Components and Modules

Antora introduces two new terms:

* **Component** — Simply put, a component is a part of the documentation website with its own menu. Components can also be versioned. In the Fedora Docs, we use separate components for user documentation, the Fedora Poject, Fedora council, Mindshare, FESCO, but also subprojects such as CommOps or Modulartity.
* **Module** — A component can be broken down into multiple modules. Modules still share a single menu on the site, but their sources can be stored in different git repositories, even owned by different groups. The default module is called "ROOT" (that's what is in this example). If you don't want to use multiple modules, only use "ROOT". But to define more modules, simply duplicate the "ROOT" directory and name it anything you want. You can store modules in one or more git repositories.

## Local preview

This repo includes scripts to build and preview the contents of this repository.

Both scripts work on Fedora (using Podman) and macOS (using Docker).

To build and preview the site, run:

```
$ ./build.sh && ./preview.sh
```

The result will be available at http://localhost:8080
