# Mòdul platform

## Introducció

El mòdul `platform` permet accedir a informació de la plataforma sobre la que s'executa el codi:
entorn Python, sistema operatiu i hardware.
Per importar-lo fem:

```python
import platform
```

Les entitats que conté són:
```
DEV_NULL, _UNIXCONFDIR, _WIN32_CLIENT_RELEASES, _WIN32_SERVER_RELEASES, __builtins__, __cached__, __copyright__, 
__doc__, __file__, __loader__, __name__, __package__, __spec__, __version__, _comparable_version, _component_re, 
_default_architecture, _dist_try_harder, _follow_symlinks, _ironpython26_sys_version_parser, 
_ironpython_sys_version_parser, _java_getprop, _libc_search, _linux_distribution, _lsb_release_version, _mac_ver_xml, 
_node, _norm_version, _parse_release_file, _platform, _platform_cache, _pypy_sys_version_parser, _release_filename, 
_release_version, _supported_dists, _sys_version, _sys_version_cache, _sys_version_parser, _syscmd_file, _syscmd_uname, 
_syscmd_ver, _uname_cache, _ver_output, _ver_stages, architecture, collections, dist, java_ver, libc_ver, 
linux_distribution, mac_ver, machine, node, os, platform, popen, processor, python_branch, python_build, python_compiler, 
python_implementation, python_revision, python_version, python_version_tuple, re, release, subprocess, sys, system, 
system_alias, uname, uname_result, version, warnings, win32_ver
```

## Funcions

* `platform()` - descripció de l'entorn amb totes les capes subjacents
* `machine()` - nom genèric del processador
* `processor()` - nom real del processador
* `system()` - nom genèric del sistema operatiu
* `version()` - versió del sistema operatiu
* `python_implementation()` - implementació de Python
* `python_version_tuple()` - tupla amb la versió de Python
