Installation
============

This app works with python 2.7, 3.4+, Django 1.10 and higher.

Recommended way to install is via pip::

  pip install django-geoip


.. _basic:

Basic
-----

* Add ``django_geoip`` to ``INSTALLED_APPS`` in settings.py::

    INSTALLED_APPS = (...
                      'django_geoip',
                      ...
                     )

* Create application tables in database::

    python manage.py migrate


* Obtain latest data to perform geoip detection by :ref:`running management command <update>`::

    python manage.py geoip_update


.. _advanced:

Advanced
--------

In order to make :ref:`user's location detection automatic <highlevel>` several other steps are required:

* Add ``LocationMiddleware`` to ``MIDDLEWARE_CLASSES``::

    MIDDLEWARE = (...
        'django_geoip.middleware.LocationMiddleware',
        ...
    )

* Provide a custom :ref:`location model <location_model>` (inherited from ``django_geoip.models.GeoLocationFacade``)

* Specify this model in :ref:`settings`::

    GEOIP_LOCATION_MODEL = 'example.models.Location' # just an example, replace with your own

* Include app urls into your urlconf if you want to :ref:`allow visitors to change their location <setlocation>`::

    urlpatterns += [
        ...
        url(r'^geoip/', include('django_geoip.urls')),
        ...
    ]

* Add local ISO codes if you want to change or add countries in :ref:`settings`::

    GEOIP_CUSTOM_ISO_CODES = {
        "RU": "Российская Федерация",
    }
