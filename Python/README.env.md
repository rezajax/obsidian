cat /usr/share/doc/python3.11/README.venv
```markdown

Installing Python Packages in Debian
====================================

It is recommended to let Debian's package managers manage Python packages in
/usr/lib/ and /usr/share/.

Python applications
-------------------

If you need to install a Python application (or version) that isn't packaged in
Debian, we recommend that you install it with pipx (in the "pipx" Debian
package). pipx will set up an environment isolated from other applications and
system Python modules, and install the application and its dependencies into
that.

Python library modules
----------------------

If you need to install a Python library module (or version) that isn't packaged
in Debian, we recommend installing it into a virtualenv, where possible. You
can create virtualenvs with the venv Python stdlib module (in the
"python3-venv" Debian package) or the virtualenv Python 3rd-party tool (in the
"virtualenv" Debian package).

Both of these will create an isolated environment, with a copy of pip in it.
After activating the environment, you can install python applications and
library modules into the virtual environment.

e.g. instead of running:
$ pip install --user foo
run:
$ mkdir -p ~/.venvs
$ python3 -m venv ~/.venvs/foo
$ ~/.venvs/foo/bin/python -m pip install foo

If needed, the isolated environment can also have access to system Python
modules, with the "--system-site-packages" flag.

Installing things system-wide
-----------------------------

Because Debian declares its Python install to be EXTERNALLY-MANAGED [0], pip
(and other installers) will refuse to install packages system-wide.
Installation is only possible in virtual environments or separate Python
installs.

[0]: https://peps.python.org/pep-0668/

This is because Python package installers (like pip) are unaware of the
constraints that APT-managed packages have on libraries and versions. See
PEP-668 for a full discussion of the problems that can occur when multiple
installers operate on the same Python install.

This can be overriden by passing the --break-system-packages option to pip. You
do this at your own risk: pip may break Python modules that part of your Debian
system depends on. This option can also be specified by exporting
PIP_BREAK_SYSTEM_PACKAGES=1 or configuring the following in
~/.config/pip/pip.conf or /etc/pip.conf:

[global]
break-system-packages = true

You can also override this system-wide by removing
/usr/lib/python3.*/EXTERNALLY-MANAGED. Again, you do this at your own risk,
with the understanding that Debian-provided Python modules may be broken by pip
/ other installers. The best way to do this is to move it with dpkg-divert,
which will survive security updates):

# dpkg-divert --rename --add /usr/lib/$(py3versions -d)/EXTERNALLY-MANAGED

A clean option is to install your own Python (from source) in /usr/local, that
isn't EXTERNALLY-MANAGED.

```

