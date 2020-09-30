# Virtual Env

Source: https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/

## On Windows
For python 3.x virtual-env is already installed with the name `venv`

#### Creating a virtual environment
To create a virtual environment, go to your project’s directory and run venv.
```sh
$ py -m venv env
```

The second argument is the location to create the virtual environment. Generally, you can just create this in your project and call it env.

venv will create a virtual Python installation in the env folder.

Note: You should exclude your virtual environment directory from your version control system using `.gitignore` or similar.

#### Activating a virtual environment
Before you can start installing or using packages in your virtual environment you’ll need to activate it. Activating a virtual environment will put the virtual environment-specific `python` and `pip` executables into your shell’s `PATH`.

```sh
$ .\env\Scripts\activate
```

#### Leaving the virtual environment
If you want to switch projects or otherwise leave your virtual environment, simply run:
```sh
$ deactivate
```
