Getting started
###############

The `minio` fixture starts a minio server using docker-compose. The `s3_content` fixture creates the bucket
if it is absent and copies the fixture files into the bucket.

.. code-block:: python

    import fixtup

    with fixtup.up('minio'), \
        fixtup.up('s3_content'):
        # the files are loaded into the s3 bucket
        # the integration tests are running
        pass


.. code-block:: yaml
    :caption: test/fixtures/minio/docker-compose.yml

    version: '3.8'
    services:
      database:
        image: quay.io/minio/minio
        command: server /data
        ports:
          - 9000:9000
          - 9001:9001


.. code-block:: yaml
    :caption: test/fixtures/s3_content/minio.yml

    minio_endpoint: http://localhost:9000
    bucket: bucket

