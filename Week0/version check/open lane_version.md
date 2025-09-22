### Quick CLI Output Verification for OpenLane

> We check the following because OpenLane relies on Python (with pip/venv) and GNU Make to run the flow, manage the virtual environment, and execute the automation. Ensuring these versions are correct avoids runtime errors during the flow.

The following outputs show the installed versions of **pip**, **GNU Make** and, **Python venv Help**:

#### pip
```text
pip 24.0 from /usr/lib/python3/dist-packages/pip (python 3.12)
```

#### GNU Make
```text
GNU Make 4.3
Built for x86_64-pc-linux-gnu
Copyright (C) 1988-2020 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
```

#### Python venv Help
```text
usage: venv [-h] [--system-site-packages] [--symlinks | --copies] [--clear] [--upgrade] [--without-pip]
            [--prompt PROMPT] [--upgrade-deps]
            ENV_DIR [ENV_DIR ...]

Creates virtual Python environments in one or more target directories.

positional arguments:
  ENV_DIR               A directory to create the environment in.

options:
  -h, --help            show this help message and exit
  --system-site-packages
                        Give the virtual environment access to the system site-packages dir.
  --symlinks            Try to use symlinks rather than copies, when symlinks are not the default for the platform.
  --copies              Try to use copies rather than symlinks, even when symlinks are the default for the platform.
  --clear               Delete the contents of the environment directory if it already exists, before environment
                        creation.
  --upgrade             Upgrade the environment directory to use this version of Python, assuming Python has been
                        upgraded in-place.
  --without-pip         Skips installing or upgrading pip in the virtual environment (pip is bootstrapped by default)
  --prompt PROMPT       Provides an alternative prompt prefix for this environment.
  --upgrade-deps        Upgrade core dependencies (pip) to the latest version in PyPI

Once an environment has been created, you may wish to activate it, e.g. by sourcing an activate script in its bin
directory.
