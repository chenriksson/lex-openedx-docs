#Open edX on Azure: Administration
---

This section is intended to help with site administration tasks.

## Administration Interfaces

* /admin
  
  URI path for the [Django admin](https://docs.djangoproject.com/en/1.9/ref/contrib/admin/) interface, accessible to superusers.

* /sysadmin
  
  URI path for the [Open edX sysadmin](https://github.com/edx/edx-platform/blob/master/lms/djangoapps/dashboard/sysadmin.py) dashboard, accessible to staff accounts.
  
  Disabled by default, but can be enabled through [configuration](configuration.md).


See [Common Tasks](docs/administration-common.md)