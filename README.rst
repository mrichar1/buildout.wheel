========================================================
Experimental Buildout extension to provide wheel support
========================================================

To get wheel support in Buildout 2.8 or later, include the buildout
wheel extension::

  [buildout]
  extensions = buildout.wheel
  ...

Wheel locations and names can be blacklisted and/or whitelisted.
If a wheel is allowed by these filters, then the wheel will be added to the list
of potential packages considered for installation.

Filtering can be achieved using the following options::

  [buildout]
  extensions = buildout.wheel
  wheel-blacklist-locations =
  wheel-whitelist-locations =
  wheel-blacklist-names =
  wheel-whitelist-names =

Each option accepts a list (new-line, or comma-separated) of regular expressions
which will be matched against the location or full wheel name (including version string).

To prevent any wheels being installed from locations whose url contains ``pypi.python.org``::

  [buildout]
  extensions = buildout.wheel
  wheel-blacklist-locations = pypi.python.org

To limit which wheels will be allowed (packages starting ``foo``,
all packages starting ``bar-1.2.3``, and packages containing ``baz-0.1.1``)::

  [buildout]
  extensions = buildout.wheel
  wheel-whitelist-names =
    ^foo
    ^bar-1\.2\.3
    baz-0\.1\.1


Whitelists take precedence over blacklists, and names take precedence over locations.

This will allow wheels from any location whose url contains ``pypi``::

  [buildout]
  extensions = buildout.wheel
  wheel-blacklist-locations = pypi.python.org
  wheel-whitelist-locations = pypi


No wheels will be allowed from pypi, except for those containing ``foo`` or ``bar``::

  [buildout]
  extensions = buildout.wheel
  wheel-blacklist-locations = pypi.python.org
  wheel-whitelist-names = foo,bar


Wheels will be allowed from pypi, but no wheels containing ``foo`` or ``bar``
will be allowed from any location::

  [buildout]
  extensions = buildout.wheel
  wheel-whitelist-locations = pypi.python.org
  wheel-blacklist-names = foo,bar
