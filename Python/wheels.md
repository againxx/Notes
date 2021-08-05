# Wheels

## A Non-wheel package
1. Download a tar.gz files (source distribution)
2. Uncompress the tarball and build a `.whl` files through a call to `setup.py`
3. Install the actual package after having built the wheel

## Source distribution
* Contain not only python code but the source code of any extension modules (such as C or C++)
* These extension modules need to be compiled at user's side 
* Source distribution also contain a bundle of metadata sitting in a directory called `<package-name>.egg-info`
    - which helps with building and installign the package
* A source distribution will get created with `python setup.py sdist`

## Wheel package
* Just download `.whl` file and install it
* Developer can create a wheel with `python setup.py bdist_wheel`

## Wheel essence
* a ZIP archived file
* a wheel filename can be broken down into several parts

> {dist}-{version}(-{build})?-{python}-{abi}-{platform}.whl

For example,

> cryptography-2.9.2-cp35-abi3-macosx_10_9_x86_64.whl
> chardet-3.0.4-py2.py3-none-any.whl

* **none** is the ABI tag, meaning the ABI isn't a factor.
* **any** is the platform, meaning this wheel will work on any platform

## Advantages
* Wheels installation is **faster**
* Wheels are typically **smaller in size**
* Installing from a source distribution runs *whatever* in that project's `setup.py`, wheels avoid this altogether
* No need for a compiler
* `pip` automatically generates `.pyc` files in the wheel that match the right Python interpreter
* Wheels provide **consistency**

## Reference
[What Are Python Wheels and Why Should You Care? – Real Python](https://realpython.com/python-wheels/)
