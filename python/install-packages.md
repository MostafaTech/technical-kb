# Installing packages
Source: https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/

Now that you’re in your virtual environment you can install packages. Let’s install the `Requests` library from the Python Package Index (PyPI):

```sh
$ pip install requests
```
pip should download requests and all of its dependencies and install them:

### Installing specific versions
pip allows you to specify which version of a package to install using version specifiers. For example, to install a specific version of `requests`:

```sh
$ pip install requests==2.18.4

# To install the latest 2.x release of requests
$ pip install requests>=2.0.0,<3.0.0

# To install pre-release versions of packages
$ pip install --pre requests
```