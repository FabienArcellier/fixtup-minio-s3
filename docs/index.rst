fixtup-minio-s3
===================================

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
