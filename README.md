<!--vale off-->
# RockyDocs runner

## Introduction

The project arose from the need to have available a *real* preview of the result of the "Material Flavoured" markdown code.  
The **mkdocs-material** plugin for the *MkDocs* documentation generator, in addition to managing the graphical appearance of the site, introduces many non-standard markdown tags that allow further customization in content formatting.  
These tags are obviously not interpreted in common markdown document preview plugins that display only the standard markdown, and consequently to display them correctly, an instance of MkDocs running with the mkdocs-material plugin installed is essential.  
This project is intended to provide a development environment where you can learn the basics of mkdocs-material tags, experiment with these tags, and test your own documents. Development takes place in an environment that fully simulates the Rocky documentation site `docs.rokydocs.org` running locally in a virtual Python environment.

The `run` script provided by the project by inputting (source) a series of functions and a menu allows all aspects of creating, installing and starting a dedicated Python virtual environment to be handled automatically.  
The script also allows you to link an arbitrary folder to the `docs` folder for developing your own documentation, greatly reducing the processing time of MkDocs when testing the graphical display.

## Installation

> [!NOTE]
> For its example installation we use a `lab` folder found in the user's home, adapt the instructions as needed if you intend to use another location.

First you need to retrieve the necessary files, so clone the repository with the command:

```bash
git clone https://github.com/ambaradan/rockydocs-runner.git ~/lab/rockydocs-runner
```

When finished we will have the new `rockydocs-runner` folder with the following structure:

```text

rockydocs-runner/
├── docs
├── rockydocs
├── mkdocs.yml
├── README.md
├── requirements.txt
├── run
├── .gitignore
└── theme
```

Inside the newly cloned folder we find two files, **mkdocs.yml** and **run**. The former is the MkDocs configuration file that will be used in the final stage of the installation (starting 'mkdocs serves') while the latter is the script that contains all the functions and menu needed to manage the **python venv + mkdocs + material** instance.  
A *.gitignore* file is also provided that hides any locally present `.venv` installations and `docs/docs` links.

> [!WARNING]
> The script as mentioned earlier needs to be entered (sourced) into bash and not executed to work properly and there is a check in the script to prevent this from happening.

Then take yourself to the cloned folder and run the source:

```bash
cd ~/lab/rockydocs-runner
source run
```

The following menu will be presented from which all operations are performed; the menu is repeated after each successful operation. Carrying out the entire procedure is necessary only on the first use after which for subsequent connections of the `docs` folder and execution of MkDocs only options 3 and 5 are used.

```text
  Installed Python version: Python 3.9.21
  Virtual environment is missing.

  Select an option
   1. Create a new virtual environment
   2. Install RockyDocs environment
   3. Create a symbolic link to an external docs folder
   4. List the current path linked to docs
   5. Run RockyDocs environment
   6. Exit
  Enter your choice [1-6]: 
```

### Creating the virtual environment

First you need to create the virtual environment (option 1) where to install *MkDocs* and the *mkdocs-material* plugin. Creating a python environment separate from the system installation allows you to run `mkdocs serve` completely independently of the global installation, thus avoiding possible conflicts between python packages.  
For its creation, the **venv** plugin provided by default by python version 3.4 or higher is used, which takes care of its creation fully automatically. Creation consists of copying a set of python system version files into the `.venv` folder plus a set of activation scripts.
Once the script has finished copying the necessary files, it displays a confirmation message and a check for any active environments.

```text
  Creating a new virtual environment...
  Virtual environment created successfully.
  No virtual environment is currently active.
```

### RockyDocs environment installation

Having created the environment it is time to install the necessary packages (option 2) , the script takes care of checking, and possibly updating *pip* (the python plugin manager) and downloading and installing all the required plugins.  
Again, a confirmation message is displayed if the operation ends successfully.

```text
  Activated the virtual environment.
  ...
  ...
  RockyDocs environment installed successfully.
  Deactivated the virtual environment.
```

### Docs folder link

The environment for previewing markdown code written in "*material flavor*" is now complete and what is missing is a folder with the contents to be displayed. You need to create a symbolic link (option 3) within the existing `docs` folder that MkDocs will later use for parsing files.

> [!TIP]
> The project provides a `rockydocs` folder with examples and explanations of the tags used by *mkdocs-material* for enriched visualization of markdown code; you can link to the example folder to get started.

```text
  Enter the path of the external folder to link: ../rockydocs/
  Removed old symbolic link 'docs'.
  Symbolic link 'docs' created pointing to '../rockydocs/'.
```

> [!NOTE]
> The script provides the auto-complete function but not the use of environment variables (`~` and `$HOME`) for path construction.

### Running RockyDocs environment

Now you are all set to preview the contents (option 5) of the `docs` folder in the browser.  
Its function consists of activating the python virtual environment and subsequent execution of `mkdocs serve`. This command locally builds a static HTML copy of markdown documents making them available on the loopback connection (*127.0.0.1*) for display in a Web browser.  
The MkDocs instance uses the *mkdocs.yml* file in the folder for its configuration, prepared as needed with all the required extensions.  

```text
  Activated the virtual environment.
  Starting mkdocs serve...
INFO    -  Building documentation...
INFO    -  Cleaning site directory
INFO    -  Documentation built in 0.32 seconds
INFO    -  [15:09:22] Watching paths for changes: 'docs', 'mkdocs.yml'
INFO    -  [15:09:22] Serving on http://127.0.0.1:8000/
```

If you have linked the `rockydocs` folder as in the suggested example you will be able to see what mkdocs-material can do to enrich and detail the documentation by opening your favorite browser at `http://127.0.0.1:8000/`.

To close the MkDocs instance and exit the virtual environment, type `Ctrl + C`

```text
^CINFO    -  Shutting down...
  Deactivated the virtual environment.
```

## Regular use

The project is designed to write primarily documentation for Rocky Linux using this plugin in the MkDocs configuration but can be used for any documentation using standard code.
To use it for your own documentation, simply replace the link to the `docs` folder, using menu option 3, by linking it to the one you are using for development. Starting MkDocs again (option 5) will give you this time at the above address a preview of your documentation.

> [!NOTE]
> The MkDocs engine constantly monitors changes to the files contained in the `docs` folder, thus enabling near-real-time visualization of the final document, so all changes made to the markdown file will be immediately made available for viewing.

## Conclusions

The entire development takes place in a separate, stand-alone environment that allows for interference-free execution; it is designed to be a tool to run alongside one's favorite editor for developing Rocky documentation by providing the editor's own extensions without the other features of the documentation site (multilingual support and more), which make it particularly heavy to process.
