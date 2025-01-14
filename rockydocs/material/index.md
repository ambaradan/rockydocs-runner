<!--vale off-->

# Material runner

## :material-book-open-blank-variant: Introduction

The project arose from the need to have available a *real* preview of the result of the "*Material Flavoured*" markdown code.  
The **mkdocs-material** plugin for the *MkDocs* documentation generator not only manages the graphical appearance of the site but also introduces many non-standard markdown tags that allow further customization for content formatting.  
These tags are obviously not interpreted in common markdown document preview plugins, and to display them properly, an instance of MkDocs running with the mkdocs-material plugin installed is essential.
This project intends to provide an automated solution to the problem, by means of the inclusion (source) of a series of functions and a menu it is possible to manage all aspects of the creation, installation and startup of a Python virtual environment where it is possible to verify the correctness of the written code.

## :material-download-outline: Installation

!!! info ""

    For its example installation we use a `lab` folder found in the user's home, adapt the instructions as needed if you intend to use another location.

First clone the repository:

```bash
git clone https://github.com/ambaradan/material-runner.git ~/lab/material-runner
```

Inside the newly cloned folder we find two files, mkdocs.yml and run. The former is the MkDocs configuration file that will be used in the final stage of the installation (starting 'mkdocs serve') while the latter is the script that contains all the functions and menu needed to manage the **python instance venv + mkdocs + material**.  
A *.gitignore* file is also provided that hides any locally present `.venv` installations and `docs` links.

!!! warning ""

    The script as mentioned above must be entered (sourced) into bash and not executed to work properly and there is a check to prevent this from happening.

Then take yourself to the cloned folder and run the source:

``` { .bash .no-copy }
cd ~/lab/material-runner
source run
```

``` { .text .no-copy title="Material runner menu" }
  Installed Python version: Python 3.9.21
  .venv directory exists.

  Select an option:
 1. Create a new virtual environment
 2. Install mkdocs-material
 3. Create a symbolic link to an external docs folder
 4. List the current path linked to docs
 5. Activate the virtual environment and run mkdocs serve
 6. Exit
  Enter your choice [1-6]: 
```

### :material-folder-plus-outline: Creating the virtual environment

First you need to create the virtual environment (option 1) where you will install MkDocs and the mkdocs-material plugin. Creating a python environment separate from the system installation allows you to run mkdocs without interfering with the global installation. For its creation, the venv plugin is used, which takes care of its creation fully automatically. Once the copying of the necessary files is finished, a confirmation message and a check for any active environments is issued.

``` { .text .no-copy }
  Creating a new virtual environment...
  Virtual environment created successfully.
  No virtual environment is currently active.
```

### :material-folder-download-outline: Installing mkdocs-material

Having created the environment it is time to install the necessary packages (option 2) , the script takes care of checking, and possibly updating pip (the python plugin manager) and downloading and installing all the required plugins.

``` { .text .no-copy }
  Activated the virtual environment.
  ...
  ...
  mkdocs-material installed successfully.
  Deactivated the virtual environment.
```

### :material-folder-sync-outline: Docs folder link

The environment for previewing the markdown code written for the `material flavor` is now complete and what is missing is a folder with the contents to be displayed. You need to create a symbolic link (option 3) to the `docs` folder that MkDocs will use for parsing files.
The project provides a `material-docs` folder with examples and explanations of the tags used by mkdocs-material for enriched visualization of markdown code; you can link to the example folder to get started.

``` { .text .no-copy }
  Enter the path of the external folder to link: material-docs/
  Removed old symbolic link 'docs'.
  Symbolic link 'docs' created pointing to 'material-docs/'.
```

NOTE: The script provides the auto-complete function but not the use of the environment variables (`~` and `$HOME`) for path construction.

### :material-folder-eye-outline: Display symbolic link

Option 4 allows you to check the path to the folder linked to the `docs` folder in case you need to.

``` { .text .no-copy }
  Current path linked to docs:
  ../material-docs/
```

### :material-folder-play-outline: Running MkDocs serve

Now everything is ready to preview the contents (option 5) of the `docs` folder in the browser, the python virtual environment will be activated and `mkdocs serve` will be executed. The MkDocs instance uses for its configuration the file mkdocs.yml, present in the folder, prepared as needed with all the required extensions.  
Open your favorite browser at `http://127.0.0.1:8000/` and you will be able to see what mkdocs-material can do to enrich and detail documentation written with the support of this plugin.

``` { .text .no-copy }
  Activated the virtual environment.
  Starting mkdocs serve...
INFO    -  Building documentation...
INFO    -  Cleaning site directory
INFO    -  Documentation built in 0.32 seconds
INFO    -  [15:09:22] Watching paths for changes: 'docs', 'mkdocs.yml'
INFO    -  [15:09:22] Serving on http://127.0.0.1:8000/
```

When you have finished testing to close the MkDocs instance, type `Ctrl + C`

``` { .text .no-copy }
^CINFO    -  Shutting down...
  Deactivated the virtual environment.
```

## :material-book-open-page-variant-outline: Regular use

The project is designed to write primarily documentation for Rocky Linux using this plugin in the MkDocs configuration but can be used for any documentation using standard code.
To use it for your own documentation, simply replace the link to the `docs` folder, using menu option 3, by linking it to the one you are using for development. Starting MkDocs again (option 4) will give you this time at the above address a preview of your documentation.

!!! info ""

    The MkDocs engine constantly monitors changes to the files contained in the `docs` folder, thus allowing for real-time visualization of the final document, so all changes made to the markdown file will be immediately made available for viewing.

## :material-book-open-variant-outline: Conclusions

The entire development takes place in a separate, stand-alone environment that allows for interference-free execution; it is designed to be a tool to run alongside one's favorite Rocky documentation development editor by providing the editor's own extensions without the other features of the documentation site (multilingual support, git review, and more), which make it particularly heavy to process.

*[MkDocs]: MkDocs is a fast and simple static site generator that's geared towards building project documentation. Documentation source files are written in Markdown, and configured with a single YAML configuration file.
*[mkdocs-material]: Material for MkDocs is a theme for MkDocs that lets you write documentation in Markdown and create a professional static site with a modern design and features
