# python-meta-names-project-package

Meta-python exercise to tease out the distinctions between the various uses of names for a project, package, and module.
# Introduction
There are at least the following uses of names that refer to the project, package, and/or module:
1. The developer-specified project name in the `name` field in `setup.cfg` or `setup.py`.
1. The project name on PyPI
1. The name used in a `pip install something` command to install the distribution-“package” created by the `build` command.
1. The name of the module-bundle “package” that immediately encloses the outermost module(s)
1. The name string by which a module is `import`ed by a script outside the package
1. The name by which the “package” is executed when using a `python -m something` command.
1. The name of the GitHub repository
1. The name of the development directory that immediately encloses `README.md`, etc.

All of these names are independently specified by the developer. However, in many projects the developer sets all of 
these names equal to a common string. It is then less than clear which name specification is being referenced when, for
example, `pip install something` is executed or, instead, `python -m something` or `import something`.

This project aims to address this lack of clarity by setting each of these names to a unique string in order to trace
back which specification is being referenced in each command.

This question takes on slightly added interest when the project name is, for readability, composed of two or more strings
joined by a delimiter such as underscore (“_”) or hyphen (“-”).

# Results
1. The developer-specified project name in the `name` field in `setup.cfg` or `setup.py`.
    * `name = meta-names-project_package`
1. The project name on PyPI
    * `meta-names-project-package`
    * This is the hyphen-normalized version of the developer-specified project name in the `name` field in `setup.cfg`
1. The name used in a `pip install something` command to install the distribution-“package” created by the `build` command.
    * This scenario is distinguished from installing the package locally with `% pip install -e .`.
1. The name of the module-bundle “package” that immediately encloses the outermost module(s)
    * `module_bundle_package`
1. The name string by which a module is `import`ed by a script outside the package
    * `import module_bundle_package`
1. The name by which the “package” is executed when using a `python -m something` command.
    * `python -m module_bundle_package`
1. The name of the GitHub repository
1. The name of the development directory that immediately encloses `README.md`, etc.
    * `python-meta-names-project-package-dev-directory`

# Conclusions
* For everthing `pip` related, the important name is the hyphen-normalized form of the developer-specified project name
in the `name` field in `setup.cfg` or `setup.py`.
    * This name need not bear any relationship to the name of the module-bundle package directory.
* For all `import`-related purposes, the crucial name is the name of the module-bundle package directory.
    * This name need not bear any relationship to the `pip`-relevant name.
* The name of the GitHub repository has no relationship to any other name.
    * However, `pip install` can be performed using the URL of the GitHub repository. In this sense, the name of the
    GitHub repository is relevant.
* The name of the development directory has no relationship to any other name.
    * Indeed, when multiple people work on the repository from multiple machines, the name of the development
    directory on any one machine can be different than the name of the development directory on any other machine.
    * The name of the development directory should, of course, communicate to the *developer* which project it
    belongs to.
    * The common practice of naming the development directory exactly the same as the module-bundle package
    directory (a) has the virtue of economy of thought (one doesn’t need to think of a different name) but
    (b) raises unnecessary and distracting questions about which directory references to that common name refer.
* The developer-specified project name in the `name` field in `setup.cfg` or `setup.py` is relevant only because it
is the *basis* for the name that PyPI associates with the project.
    * However, PyPI will replace any run of underscores (“_”), hyphens (“-”), and periods (“.”) with a single hyphen.
    * Thus there is no reason not to pre-normalize the developer-specified project name. Pre-normalizing this name
    will prevent any confusion that would arise when the developer-specified project name is not identical to the
    PyPI name.