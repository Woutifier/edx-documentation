.. _Install and Start ECommerce:

########################################
Install and Start the E-Commerce Service
########################################

To install and start the edX E-Commerce service, you must complete the
following steps.

.. contents::
   :depth: 1
   :local:

.. note::
 These steps assume that you are running Open edX `devstack`_. If you prefer to
 run the E-Commerce service locally on your computer instead of on the virtual
 machine (VM) that devstack uses, see :ref:`Development Outside Devstack`.

.. _Set Up a Virtual Environment:

****************************
Set Up a Virtual Environment
****************************

#. Create or activate a Python virtual environment. You execute all of the
   commands described in this section within the virtualenv (unless otherwise
   noted).

   For more information, see `Virtual Environments`_.

#. Run the following command to install dependencies.

   .. code-block:: bash

    $ make requirements

#. (Optional) Create settings overrides that you do not commit to the
   repository. To do this, create a file named
   ``ecommerce/settings/private.py``. The ``ecommerce/settings/local.py`` file
   reads the values in this file, but Git ignores the file.

.. _Run Migrations:

**************
Run Migrations
**************

To setup the ``ecommerce`` database, you must run migrations.

.. note::
    Local installations use SQLite by default. If you use another database
    backend, make sure you update your settings and create the database, if
    necessary, before you run migrations.

#. To run migrations, execute the following command.

   .. code-block:: bash

      $ make migrate

.. _Configure OIDC:

***********************************
Configure edX OpenID Connect (OIDC)
***********************************

The E-Commerce service relies on the edX `OpenID Connect`_ (OIDC)
authentication provider for login. OIDC is built on top of OAuth 2.0.
Currently, the LMS serves as the authentication provider.

To configure the E-Commerce service to work with OIDC, complete the following
procedures.

.. contents::
   :depth: 1
   :local:

.. _Create Register Client:

============================
Create and Register a Client
============================

To create and register a new OIDC client, follow these steps.

#. Start the LMS.
#. In your browser, go to ``http://127.0.0.1:8000/admin/oauth2/client/``.
#. Select **Add client**.
#. Leave the **User** field blank.
#. For **Client Name**, enter ``E-Commerce Service``.
#. For **URL**, enter ``http://localhost:8002/``.
#. For **Redirect URL**, enter ``https://localhost:8002/complete/edx-oidc/``.
   This is the OIDC client endpoint.

   The system automatically generates values in the **Client ID** and **Client
   Secret** fields. You use these values when you :ref:`update Django
   settings<Update Django Settings>`.

#. For **Client Type**, select **Confidential (Web applications)**.
#. Select **Save**.

===============================
Designate the Client as Trusted
===============================

After you create your client, designate it as trusted. Trusted clients
bypass the user consent form that usually appears after the system validates
the user's credentials.

To designate your client as trusted, follow these steps.

#. In your browser, go to
   ``http://127.0.0.1:8000/admin/oauth2_provider/trustedclient/add/``.
#. In the **OAuth 2.0 clients** list, select the redirect URL for the client
   that you just created.
#. Select **Save**.

.. _Update Site, Partner, and SiteConfiguration:

***********************************************
Configure Site, Partner, and Site Configuration
***********************************************

To finish creating and configuring your OIDC client, you must configure a
partner, site, and site configuration for the E-Commerce service to use.
There is a default site that was added to the service when you ran migrations
above. You must update this site to match the domain by which you will be
accessing the E-Commerce service. You must also configure a site configuration
that contains an ``oauth_settings`` JSON field which stores your OIDC client's
settings described below.

.. list-table::
   :widths: 25 60 20
   :header-rows: 1

   * - Setting
     - Description
     - Value
   * - ``SOCIAL_AUTH_EDX_OIDC_KEY``
     - OAuth 2.0 client key
     - The **Client ID** field in the :ref:`Create
       Register Client` section.
   * - ``SOCIAL_AUTH_EDX_OIDC_SECRET``
     - OAuth 2.0 client secret
     - The value from the **Client Secret** field in the :ref:`Create
       Register Client` section.
   * - ``SOCIAL_AUTH_EDX_OIDC_URL_ROOT``
     - OAuth 2.0 authentication URL
     - For example, ``http://127.0.0.1:8000/oauth2``.
   * - ``SOCIAL_AUTH_EDX_OIDC_ID_TOKEN_DECRYPTION_KEY``
     - OIDC ID token decryption key, used to validate the ID
       token
     - The same value as ``SOCIAL_AUTH_EDX_OIDC_SECRET``.

To configure your default site, partner, and site configuration, follow these steps.

#. (Devstack only) If you are using devstack, use the ``ecommerce.settings.devstack``
   settings module to run the following Django management command which will update the
   default site and create a new partner and site configuration with the specified options.

    .. code-block:: bash

      $ sudo su ecommerce
      $ python manage.py create_or_update_site --site-id=1 --site-domain=127.0.0.1:8002 --partner-code=edX --partner-name='Open edX' --lms-url-root=http://127.0.0.1:8000 --theme-scss-path=sass/themes/edx.scss --payment-processors=cybersource,paypal --client-id=[change to OIDC client ID] --client-secret=[change to OIDC client secret]

You can also use the ``create_or_update_site`` command, to add additional
sites, partners, and site configurations. The available options you can
provide when running the command are described below.

.. list-table::
   :widths: 25 60 20
   :header-rows: 1

   * - Option
     - Description
     - Example
   * - ``--site-id``
     - Database ID of a site you want to update
     - ``--site-id=1``
   * - ``--site-domain``
     - **Required** Domain by which you will access
       the E-Commerce service
     - ``--site-domain=ecommerce.example.com``
   * - ``--site-name``
     - Name of the E-Commerce site
     - ``--site-name='Example E-Commerce'``
   * - ``--partner-code``
     - **Required** Short code of the partner
     - ``--partner-code=edX``
   * - ``--partner-name``
     - Name of the partner
     - ``--partner-name='Open edX'``
   * - ``--lms-url-root``
     - **Required** URL root of the Open edX LMS instance
     - ``--lms-url-root=https://example.com``
   * - ``--theme-scss-path``
     - ``STATIC_ROOT`` relative path of the site's SCSS file
     - ``--theme-scss-path=sass/themes/edx.scss``
   * - ``--payment-processors``
     - Comma-delimited list of payment processors used on the site
     - ``--payment-processors=cybersource,paypal``
   * - ``--client-id``
     - **Required** OIDC client ID
     - ``--client-id=ecommerce-key``
   * - ``--client-secret``
     - **Required** OIDC client secret
     - ``--client-id=ecommerce-secret``

To add an additional site, follow these steps.

#. (Devstack only) If you are using devstack, use the ``ecommerce.settings.devstack``
   settings module to run the following Django management command which will create
   new site, partner, and site configuration with the specified options.

    .. code-block:: bash

      $ sudo su ecommerce
      $ python manage.py create_or_update_site --site-domain=[change me] --partner-code=[change me] --partner-name=[change me] --lms-url-root=[change me] --client-id=[OIDC client ID] --client-secret=[OIDC client secret]

****************
Start the Server
****************

To complete the installation and start the E-Commerce service, follow these
steps.

.. note::
    Local installations use SQLite by default. If you use another database
    backend, make sure you update your settings and create the database, if
    necessary, before you run migrations.

#. (Devstack only) If you are using devstack, switch to the ``ecommerce`` user
   and use the ``ecommerce.settings.devstack`` settings module to run the
   following commands.

    .. code-block:: bash

      $ sudo su ecommerce
      $ make devserve

#. To run the server, execute the following command.

   .. code-block:: bash

     $ python manage.py runserver 8002

   .. note::
     If you use a different port, make sure you update the OIDC client by using
     the Django administration panel in the LMS. For more information about
     configuring the OIDC client, see :ref:`Configure OIDC`.



.. _Development Outside Devstack:

****************************
Development Outside Devstack
****************************

If you are running the LMS in `devstack`_ but would prefer to run the
E-Commerce service on your host, set up a reverse port-forward. This reverse
port-forward allows the LMS process inside your devstack to use
``127.0.0.1:8002`` to make calls to the E-Commerce service running on your
host. This simplifies LMS URL configuration.

To set up a reverse port-forward, execute the following command when you SSH
into your devstack. Make sure that you run this command on the VM host, not the
guest.

.. code-block:: bash

    $ vagrant ssh -- -R 8002:127.0.0.1:8002




.. include:: ../../../links/links.rst
