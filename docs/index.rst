fixtup-minio-s3
===============


.. image:: https://img.shields.io/pypi/v/fixtup-minio-s3.svg?label=Version
    :target: https://pypi.org/project/fixtup-minio-s3/

.. image:: https://github.com/FabienArcellier/fixtup-minio-s3/actions/workflows/main.yml/badge.svg
    :target: https://github.com/FabienArcellier/fixtup-minio-s3/actions/workflows/main.yml

.. image:: https://readthedocs.org/projects/fixtup-minio-s3/badge/?version=latest
    :target: https://fixtup-minio-s3.readthedocs.io/en/latest/?badge=latest

.. image:: https://img.shields.io/badge/discord-fixtup-5865F2?logo=discord&logoColor=white
    :target: https://discord.gg/nMn9YPRGSY

.. image:: https://img.shields.io/badge/license-MIT-007EC7.svg
    :target: https://github.com/FabienArcellier/fixtup-minio-s3/blob/master/LICENSE


The ``fixtup-minio-s3`` plugin allows you to download the files of a fixture into an s3 bucket managed by minio
and run the integration tests on an s3 bucket.

The plugin also allows you to manage the life cycle of the bucket on which the files are loaded by recreating
it between each test or by emptying it between each test.

.. code-block:: python
    :caption: tests/integrations/test_s3_sdk.py

    import fixtup

    with fixtup.up('minio'), \
        fixtup.up('s3_content'):
        # the files are loaded into the s3 bucket
        # the integration tests are running
        pass


Once the plugin is installed and activated in fixtup, we declare the ``minio.yml`` manifest in a fixture so
that it loads the files into an s3 bucket when launched.

.. code-block:: yaml
    :caption: tests/fixtures/s3_content/minio.yml

    minio_endpoint: http://localhost:9000 # [optional], default : http://localhost:9000
    authentification: minioadmin:minioadmin # [optional], default : minioadmin:minioadmin
    bucket: bucket # [optional], default : bucket
    setup_data_bucket_policy: new_bucket | clear_bucket | none # [optional], default : new_bucket
    copy_ignore: [] # [optional], default : []

By default, all files in a fixture are copied to s3. It is possible to exclude
some of them using the ``copy_ignore`` parameter

.. code-block:: yaml
    :caption: tests/fixtures/s3_content/minio.yml

    copy_ignore:
      - 'file.svg'
      - '**/*.svg'

.. toctree::
   :maxdepth: 1

   installation
   getting_started
   api

Links
-----

* Source code: https://github.com/FabienArcellier/fixtup-minio-s3
* PyPI Release : https://pypi.org/project/fixtup-minio-s3
* Documentation : https://fixtup-minio-s3.readthedocs.io/en/latest
* Chat: https://discord.gg/nMn9YPRGSY

