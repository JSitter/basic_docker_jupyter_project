# Basic Docker Jupyter Notebook Project
This project uses Docker to manage the dependencies required by Jupyter Notebooks. Instead of trying to fiddle with creating and managing python environments using pip or virtualenv, Docker will install any requirements listed in jupyter/requirements.txt into the container that runs the notebooks.

# Installation
Docker is required for installation and can be installed by following the installation instructions [here](https://docs.docker.com/install/).

This project needs to be built before it can be run. While inside the project directory run:

```
$ docker-compose build
```

Followed by 

```
$ docker-compose up
```

You should see the confirmation:

```
Attaching to jupyter_container
jupyter_container | Set username to: jovyan
jupyter_container | usermod: no changes
jupyter_container | Executing the command: jupyter notebook
jupyter_container | [I 17:18:15.255 NotebookApp] Writing notebook server cookie secret to /home/jovyan/.local/share/jupyter/runtime/notebook_cookie_secret
jupyter_container | [I 17:18:17.563 NotebookApp] JupyterLab extension loaded from /opt/conda/lib/python3.7/site-packages/jupyterlab
jupyter_container | [I 17:18:17.563 NotebookApp] JupyterLab application directory is /opt/conda/share/jupyter/lab
jupyter_container | [I 17:18:17.567 NotebookApp] Serving notebooks from local directory: /home/jovyan
jupyter_container | [I 17:18:17.567 NotebookApp] The Jupyter Notebook is running at:
jupyter_container | [I 17:18:17.567 NotebookApp] http://(1ceed88500b1 or 127.0.0.1):8888/?token=6e6bff61b8b447b57639d1cc316493d94149c98dc934ed5b
jupyter_container | [I 17:18:17.567 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
```

In order to connect to the notebook you'll need to supply the token that is given to you on startup. In this example you would visit `http://127.0.0.1::8888/?token=6e6bff61b8b447b57639d1cc316493d94149c98dc934ed5b` in your browser to work with the notebook.

## Creating Notebooks

In order for your work to be saved, your notebooks must exist in the notebooks directory. This directory is shared with the host system which means that when you stop, or rebuild the Docker container all your work will be saved. If you put your notebooks elsewhere there is no guarantee you'll be able to access your work later.

## Using Datasets

The datasets folder exists in its own separate Docker volume. Any dataset that you add to this folder will be available to your notebooks in the dataset folder.

## Adding project dependencies

In order to add additional dependencies to your project edit `jupyter/requirements.txt` to add the desired dependency. Afterwards the container must be rebuilt by running `docker-compose build` followed by `docker-compose up`. Your new dependencies should be available to your project