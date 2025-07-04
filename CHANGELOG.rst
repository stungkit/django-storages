django-storages CHANGELOG
=========================

X.YY.Z (UNRELEASED)
*******************

General
-------

- Add support for Django 5.2

1.14.6 (2025-04-01)
*******************

Google Cloud
------------

- Add option to sign URLs via IAM Blob API (`#1427`_)

S3
--

- Fix ``exists`` calls when using SSE-C (`#1451`_)
- Default ``url_protocol`` to ``https:`` if set to ``None`` (`#1483`_)

.. _#1427: https://github.com/jschneier/django-storages/pull/1427
.. _#1451: https://github.com/jschneier/django-storages/pull/1451
.. _#1483: https://github.com/jschneier/django-storages/pull/1483

1.14.5 (2025-02-15)
*******************

General
-------

- Revert ``exists()`` behavior to pre-1.14.4 semantics with additional hardening for Django versions < 4.2 to fix
  CVE-2024-39330. This change matches the eventual behavior Django itself shipped with. (`#1484`_, `#1486`_)
- Add support for Django 5.1 (`#1444`_)

Azure
-----

- **Deprecated**: The setting ``AZURE_API_VERSION/api_version`` setting is deprecated in favor of
  the new ``AZURE_CLIENT_OPTIONS`` setting. A future version will remove support for this setting.
- Add ``AZURE_CLIENT_OPTIONS`` settings to enable customization of all ``BlobServiceClient`` parameters
  such as ``api_version`` and all ``retry*`` options. (`#1432`_)

Dropbox
-------

- As part of the above hardening fix a bug was uncovered whereby a ``root_path`` setting would be applied
  multiple times during ``save()`` (`#1484`_)
- Fix setting OAuth2 access token via env var (`#1452`_)

FTP
---

- Fix incorrect ``exists()`` results due to an errant appended slash (`#1438`_)

Google Cloud
------------

- Switch checksum to ``crc32c`` to fix downloading when running in FIPS mode (`#1473`_)
- Fix double decompression when using ``gzip`` (`#1457`_)


.. _#1484: https://github.com/jschneier/django-storages/pull/1484
.. _#1486: https://github.com/jschneier/django-storages/pull/1486
.. _#1444: https://github.com/jschneier/django-storages/pull/1444
.. _#1432: https://github.com/jschneier/django-storages/pull/1432
.. _#1473: https://github.com/jschneier/django-storages/pull/1473
.. _#1457: https://github.com/jschneier/django-storages/pull/1457
.. _#1452: https://github.com/jschneier/django-storages/pull/1452
.. _#1438: https://github.com/jschneier/django-storages/pull/1438


1.14.4 (2024-07-09)
*******************

S3
--

- Pull ``AWS_SESSION_TOKEN`` from the environment (`#1399`_)
- Fix newline handling for text mode files (`#1381`_)
- Do not sign URLs when ``querystring_auth=False`` e.g public buckets or static files (`#1402`_)
- Cache CloudFront Signers (`#1417`_)

Azure
-----

- Fix ``collectstatic --clear`` (`#1403`_)
- Add ``mode`` kwarg to ``.url()`` to support creation of signed URLs for upload (`#1414`_)
- Fix fetching user delegation key when custom domain is enabled (`#1418`_)

SFTP
----

- Add implementations of ``get_(modified|accessed)_time`` (`#1347`_)

Dropbox
-------

- Add support for Python 3.12 (`#1421`_)

FTP
---

- Conform to ``BaseStorage`` interface (`#1423`_)
- Add ``FTP_ALLOW_OVERWRITE`` setting (`#1424`_)

.. _#1399: https://github.com/jschneier/django-storages/pull/1399
.. _#1381: https://github.com/jschneier/django-storages/pull/1381
.. _#1402: https://github.com/jschneier/django-storages/pull/1402
.. _#1403: https://github.com/jschneier/django-storages/pull/1403
.. _#1414: https://github.com/jschneier/django-storages/pull/1414
.. _#1417: https://github.com/jschneier/django-storages/pull/1417
.. _#1418: https://github.com/jschneier/django-storages/pull/1418
.. _#1347: https://github.com/jschneier/django-storages/pull/1347
.. _#1421: https://github.com/jschneier/django-storages/pull/1421
.. _#1423: https://github.com/jschneier/django-storages/pull/1423
.. _#1424: https://github.com/jschneier/django-storages/pull/1424


1.14.3 (2024-05-04)
*******************

General
-------

- Add support for Django 5.0 and Python 3.12 (`#1331`_)

S3
--

- **Deprecated**: The ``config`` class property has been deprecated in favor of the ``client_config`` setting,
  a future version will remove support for the property.
- Fix disabling CloudFront signing with class variables (`#1334`_)
- Fix ``AWS_S3_*`` environment variables lookup (`#1336`_)
- Add ``client_config/AWS_S3_CLIENT_CONFIG`` to configure advanced ``botocore`` settings (`#1386`_)

Google Cloud
------------

- Fix re-gzipping already gzipped files (`#1366`_)

SFTP
----

- Add ``SFTP_BASE_URL`` setting (`#1368`_)
- Fix saving files when ``SFTP_STORAGE_ROOT`` is set (`#1372`_)

FTP
---

- Add support for FTP TLS via ``ftps`` URLs (`#1320`_)
- Add support for passwords with urlchars (`#1329`_)

.. _#1331: https://github.com/jschneier/django-storages/pull/1331
.. _#1386: https://github.com/jschneier/django-storages/pull/1386
.. _#1372: https://github.com/jschneier/django-storages/pull/1372
.. _#1334: https://github.com/jschneier/django-storages/pull/1334
.. _#1336: https://github.com/jschneier/django-storages/pull/1336
.. _#1366: https://github.com/jschneier/django-storages/pull/1366
.. _#1368: https://github.com/jschneier/django-storages/pull/1368
.. _#1320: https://github.com/jschneier/django-storages/pull/1320
.. _#1329: https://github.com/jschneier/django-storages/pull/1329

1.14.2 (2023-10-08)
*******************

S3
--

- Fix re-opening of ``S3File`` (`#1321`_)
- Revert raising ``ImproperlyConfigured`` when no ``bucket_name`` is set (`#1322`_)

.. _#1321: https://github.com/jschneier/django-storages/pull/1321
.. _#1322: https://github.com/jschneier/django-storages/pull/1322

1.14.1 (2023-09-29)
*******************

Azure
-----

- Do not require both ``AccountName`` and ``AccountKey`` in ``connection_string`` (`#1312`_)

S3
--

- Work around boto3 closing the uploaded file (`#1303`_)
- Fix crash when cleaning up during aborted connection of ``S3File.write`` (`#1304`_)
- Raise ``FileNotFoundError`` when attempting to read the ``size`` of a non-existent file (`#1309`_)
- Move auth & CloudFront signer validation to init (`#1302`_)
- Raise ``ImproperlyConfigured`` if no ``bucket_name`` is set (`#1313`_)
- Fix tracking of ``S3File.closed`` (`#1311`_)

.. _#1303: https://github.com/jschneier/django-storages/pull/1303
.. _#1304: https://github.com/jschneier/django-storages/pull/1304
.. _#1309: https://github.com/jschneier/django-storages/pull/1309
.. _#1302: https://github.com/jschneier/django-storages/pull/1302
.. _#1313: https://github.com/jschneier/django-storages/pull/1313
.. _#1312: https://github.com/jschneier/django-storages/pull/1312
.. _#1311: https://github.com/jschneier/django-storages/pull/1311

1.14 (2023-09-04)
*******************

General
-------

- **Breaking**: Drop support for Django 4.0 (`#1235`_)
- **Breaking**: The long deprecated & removed (from Django) ``(modified|created|accessed)_time`` methods have been
  removed from the various storages, please replace with the ``get_(modified|created|accessed)_time`` methods
- Add support for saving ``pathlib.PurePath`` names (`#1278`_)
- Add support for Django 4.2 (`#1236`_)

Azure
-----

- Set ``account_(name|key)`` from ``connection_string`` if not provided (`#1225`_)

Dropbox
-------

- **Deprecated:** The name ``DropboxStorage.location`` has been deprecated, please rename to ``DropboxStorage.root_path``, a future version will
  remove support for the old name. (`#1251`_)
- Storage and related names with a captialized B have been changed to no longer have one e.g ``DropboxStorage`` has now replaced
  ``DropBoxStorage``. Aliases have been added so no change is necessary at this time. A future version might deprecate the old names. (`#1250`_)
- ``DropboxStorage`` now conforms to the ``BaseStorage`` interface (`#1251`_)
- Fix name mangling when saving with certain complex root paths (`#1279`_)

FTP
---

- Use setting ``BASE_URL`` if it is defined (`#1238`_)

Google Cloud
------------

- **Breaking**: Support for the deprecated ``GS_CACHE_CONTROL`` has been removed. Please set the ``cache_control`` parameter of
  ``GS_OBJECT_PARAMETERS`` instead. (`#1220`_)

Libcloud
--------

- Reading a file that does not exist will now raise ``FileNotFoundError`` (`#1191`_)

SFTP
----

- Add closing context manager for standalone usage to ensure connections are cleaned up (`#1253`_)

S3
--

- **Deprecated:** ``AWS_S3_USE_THREADS`` has been deprecated in favor of ``AWS_S3_TRANSFER_CONFIG`` (`#1280`_)
- **Important:** The namespace of this backend has changed from ``S3Boto3`` to ``S3``. There are no current plans
  to deprecate and remove the old namespace but please update if you can. All paths, imports, and classes that previously
  referred to ``s3boto`` are now ``s3``. E.g ``S3Boto3Storage`` has been changed to ``S3Storage`` and ``S3Boto3StorageFile``
  has been changed to ``S3File``. (`#1289`_). Additionally the install extra is now ``s3`` (`#1284`_)
- Add setting ``transfer_config/AWS_S3_TRANSFER_CONFIG`` to customize any of the ``TransferConfig`` properties (`#1280`_)
- Enable passing ``security_token`` to constructor (`#1246`_)
- Do not overwrite a returned ``ContentType`` from ``get_object_parameters`` (`#1281`_)
- Add support for setting ``cloudfront_key_id`` and ``cloudfront_key`` via Django 4.2's ``OPTIONS`` (`#1274`_)
- Fix ``S3File.closed`` (`#1249`_)
- Fix opening new files in write mode with ``S3File`` (`#1282`_)
- Fix ``S3File`` not respecting mode on ``readlines`` (`#1000`_)
- Fix saving files with string content (`#911`_)
- Fix retrieving files with SSE-C enabled (`#1286`_)

.. _#1280: https://github.com/jschneier/django-storages/pull/1280
.. _#1289: https://github.com/jschneier/django-storages/pull/1289
.. _#1284: https://github.com/jschneier/django-storages/pull/1284
.. _#1274: https://github.com/jschneier/django-storages/pull/1274
.. _#1281: https://github.com/jschneier/django-storages/pull/1281
.. _#1282: https://github.com/jschneier/django-storages/pull/1282
.. _#1279: https://github.com/jschneier/django-storages/pull/1279
.. _#1278: https://github.com/jschneier/django-storages/pull/1278
.. _#1235: https://github.com/jschneier/django-storages/pull/1235
.. _#1236: https://github.com/jschneier/django-storages/pull/1236
.. _#1225: https://github.com/jschneier/django-storages/pull/1225
.. _#1251: https://github.com/jschneier/django-storages/pull/1251
.. _#1250: https://github.com/jschneier/django-storages/pull/1250
.. _#1238: https://github.com/jschneier/django-storages/pull/1238
.. _#1220: https://github.com/jschneier/django-storages/pull/1220
.. _#1191: https://github.com/jschneier/django-storages/pull/1191
.. _#1253: https://github.com/jschneier/django-storages/pull/1253
.. _#1246: https://github.com/jschneier/django-storages/pull/1246
.. _#1249: https://github.com/jschneier/django-storages/pull/1249
.. _#1000: https://github.com/jschneier/django-storages/pull/1000
.. _#911: https://github.com/jschneier/django-storages/pull/911
.. _#1286: https://github.com/jschneier/django-storages/pull/1286

1.13.2 (2022-12-23)
*******************

General
-------

- Add support for Python 3.11 (`#1196`_)
- Add support for saving ``pathlib.Path`` names (`#1200`_)

S3
--

- Catch 404 errors when calling ``delete()`` (`#1201`_)

Azure
-----

- Use ``AZURE_CUSTOM_DOMAIN`` for retrieving blob URLs and storage URL for other operations (`#1176`_)

Google Cloud
------------

- Use ``DEFAULT_RETRY`` for all upload & delete operations (`#1156`_)
- Fix gzipping of content (`#1203`_)
- Pass through kwargs to signed URL generator (`#1193`_)

SFTP
----

- Improve write & memory performance when saving files (`#1194`_)

.. _#1196: https://github.com/jschneier/django-storages/pull/1196
.. _#1200: https://github.com/jschneier/django-storages/pull/1200
.. _#1201: https://github.com/jschneier/django-storages/pull/1201
.. _#1176: https://github.com/jschneier/django-storages/pull/1176
.. _#1156: https://github.com/jschneier/django-storages/pull/1156
.. _#1203: https://github.com/jschneier/django-storages/pull/1203
.. _#1193: https://github.com/jschneier/django-storages/pull/1193
.. _#1194: https://github.com/jschneier/django-storages/pull/1194

1.13.1 (2022-08-06)
*******************

Dropbox
-------

- Strip off the root path when saving files to fix saving with upgraded versions of Django (`#1168`_)
- Update ``DropBoxStorage`` constructor parameter order to be backwards compatible (`#1167`_)

.. _#1167: https://github.com/jschneier/django-storages/pull/1167
.. _#1168: https://github.com/jschneier/django-storages/pull/1168

1.13 (2022-08-05)
*****************

General
-------

- Add support for Django 4.0 and 4.1 (`#1093`_)
- Drop support for Django 2.2, 3.0 and 3.1 (`#1093`_)
- Drop support for Python 3.5 and 3.6 (`#1093`_)

S3
--

- **Breaking**: Update and document the undocumented ``AWS_S3_URL_PROTOCOL`` from ``http:`` to ``https:`` and remove the
  undocumented ``AWS_S3_SECURE_URLS`` setting. You should only need to update your settings if you had updated either of
  these previously undocumented settings.  The default behavior of constructing an ``https:`` URL with a custom domain
  is unchanged (`#1164`_)
- Add ``AWS_S3_USE_THREADS`` to disable ``threading`` for compatibility with ``gevent`` (`#1112`_)

Dropbox
-------

- Add support for refresh tokens (`#1159`_)
- Ignore ``ApiError`` exception in ``url()`` (`#1158`_)

Azure
-----

- Restore support for ``AZURE_ENDPOINT_SUFFIX`` (`#1118`_)
- Replace deprecated ``download_to_stream`` with ``readinto`` (`#1113`_)
- Add ``AZURE_API_VERSION`` setting (`#1132`_)
- Fix ``get_modified_time()`` (`#1134`_)

Google Cloud
------------

- Add support for gzipping files via ``GS_IS_GZIPPED`` and ``GZIP_CONTENT_TYPES`` (`#980`_)
- Use ``GS_BLOB_CHUNK_SIZE`` with files that already exist (`#1154`_)

.. _#980: https://github.com/jschneier/django-storages/pull/980
.. _#1118: https://github.com/jschneier/django-storages/pull/1118
.. _#1113: https://github.com/jschneier/django-storages/pull/1113
.. _#1112: https://github.com/jschneier/django-storages/pull/1112
.. _#1132: https://github.com/jschneier/django-storages/pull/1132
.. _#1134: https://github.com/jschneier/django-storages/pull/1134
.. _#1159: https://github.com/jschneier/django-storages/pull/1159
.. _#1158: https://github.com/jschneier/django-storages/pull/1158
.. _#1164: https://github.com/jschneier/django-storages/pull/1164
.. _#1093: https://github.com/jschneier/django-storages/pull/1093
.. _#1154: https://github.com/jschneier/django-storages/pull/1154


1.12.3 (2021-10-29)
*******************

General
-------

- Add support for Python 3.10 (`#1078`_)

S3
--

- Re-raise non-404 errors in ``.exists()`` (`#1084`_, `#1085`_)

Azure
-----

- Fix using ``AZURE_CUSTOM_DOMAIN`` with an account key credential (`#1082`_, `#1083`_)

SFTP
----

- Catch ``FileNotFoundError`` instead of ``OSerror`` in ``.exists()`` to prevent swallowing ``socket.timeout`` exceptions (`#1064`_, `#1087`_)


.. _#1078: https://github.com/jschneier/django-storages/pull/1078
.. _#1084: https://github.com/jschneier/django-storages/issues/1084
.. _#1085: https://github.com/jschneier/django-storages/pull/1085
.. _#1082: https://github.com/jschneier/django-storages/issues/1082
.. _#1083: https://github.com/jschneier/django-storages/pull/1083
.. _#1064: https://github.com/jschneier/django-storages/issues/1064
.. _#1087: https://github.com/jschneier/django-storages/pull/1087

1.12.2 (2021-10-16)
*******************

Azure
-----

- Add ``parameters`` kwarg to ``AzureStorage.url`` to configure blob properties in the SAS token (`#1071`_)
- Fix regression where ``AZURE_CUSTOM_DOMAIN`` was interpreted as a replacement of ``blob.core.windows.net`` rather than as a full domain
  (`#1073`_, `#1076`_)

.. _#1071: https://github.com/jschneier/django-storages/pull/1071
.. _#1073: https://github.com/jschneier/django-storages/issues/1073
.. _#1076: https://github.com/jschneier/django-storages/pull/1076

1.12.1 (2021-10-11)
*******************

S3
--

- Change gzip compression to use a streaming implementation (`#1061`_)
- Fix saving files with ``S3ManifestStaticStorage`` (`#1068`_, `#1069`_)

.. _#1061: https://github.com/jschneier/django-storages/pull/1061
.. _#1068: https://github.com/jschneier/django-storages/issues/1068
.. _#1069: https://github.com/jschneier/django-storages/pull/1069

1.12 (2021-10-06)
*****************

General
-------
- Add support for Django 3.2 (`#1046`_, `#1042`_, `#1005`_)
- Replace Travis CI with GitHub actions (`#1051`_)

S3
--

- Convert signing keys to bytes if necessary (`#1003`_)
- Avoid a ListParts API call during multipart upload (`#1041`_)
- Custom domains now use passed URL params (`#1054`_)
- Allow the use of AWS profiles and clarify the options for passing credentials (`fbe9538`_)
- Re-allow override of various access key names (`#1026`_)
- Properly exclude empty folders during ``listdir`` (`66f4f8e`_)
- Support saving file objects that are not ``seekable`` (`#860`_, `#1057`_)
- Return ``True`` for ``.exists()`` if a non-404 error is encountered (`#938`_)

Azure
-----

- **Breaking**: This backend has been rewritten to use the newer versions of ``azure-storage-blob``, which now has a minimum required version of 12.0. The settings ``AZURE_EMULATED_MODE``, ``AZURE_ENDPOINT_SUFFIX``, and ``AZURE_CUSTOM_CONNECTION_STRING`` are now ignored. (`#784`_, `#805`_)
- Add support for user delegation keys (`#1063`_)

Google Cloud
------------

- **Breaking**: The minimum required version of ``google-cloud-storage`` is now 1.27.0 (`#994`_)
- **Breaking**: Switch URL signing version from v2 to v4 (`#994`_)
- **Deprecated**: Support for ``GS_CACHE_CONTROL`` will be removed in 1.13. Please set the ``cache_control`` parameter of ``GS_OBJECT_PARAMETERS`` instead. (`#970`_)
- Add ``GS_OBJECT_PARAMETERS`` and overridable ``GoogleCloudStorage.get_object_parameters`` to customize blob parameters for all blobs and per-blob respectively. (`#970`_)
- Catch the ``NotFound`` exception raised when deleting a non-existent blob, this matches Django and other backends (`#998`_, `#999`_)
- Fix signing URLs with custom endpoints (`#994`_)

Dropbox
-------

- Validate ``write_mode`` param (`#1020`_)

.. _fbe9538: https://github.com/jschneier/django-storages/commit/fbe9538b8574cfb0d95b04c9c477650dbfe8547b
.. _66f4f8e: https://github.com/jschneier/django-storages/commit/66f4f8ec68daaac767c013d6b1a30cf26a7ac1ca
.. _#1003: https://github.com/jschneier/django-storages/pull/1003
.. _#1054: https://github.com/jschneier/django-storages/pull/1054
.. _#1026: https://github.com/jschneier/django-storages/pull/1026
.. _#1041: https://github.com/jschneier/django-storages/pull/1041
.. _#970: https://github.com/jschneier/django-storages/pull/970
.. _#998: https://github.com/jschneier/django-storages/issues/998
.. _#784: https://github.com/jschneier/django-storages/issues/784
.. _#805: https://github.com/jschneier/django-storages/pull/805
.. _#999: https://github.com/jschneier/django-storages/pull/999
.. _#1051: https://github.com/jschneier/django-storages/pull/1051
.. _#1042: https://github.com/jschneier/django-storages/pull/1042
.. _#1046: https://github.com/jschneier/django-storages/issues/1046
.. _#1005: https://github.com/jschneier/django-storages/pull/1005
.. _#1020: https://github.com/jschneier/django-storages/pull/1020
.. _#860: https://github.com/jschneier/django-storages/issues/860
.. _#1057: https://github.com/jschneier/django-storages/pull/1057
.. _#938: https://github.com/jschneier/django-storages/pull/938
.. _#994: https://github.com/jschneier/django-storages/pull/994
.. _#1063: https://github.com/jschneier/django-storages/pull/1063

1.11.1 (2020-12-23)
*******************

S3
--

- Revert fix for ``ValueError: I/O operation on closed file`` when calling ``collectstatic`` and
  introduce ``S3StaticStorage`` and ``S3ManifestStaticStorage`` for use as ``STATICFILES_STORAGE`` targets (`#968`_)

.. _#968: https://github.com/jschneier/django-storages/pull/968

1.11 (2020-12-16)
*****************

General
-------

- Test against Python 3.9 (`#964`_)

S3
--

- Fix ``ValueError: I/O operation on closed file`` when calling ``collectstatic`` (`#382`_, `#955`_)
- Calculate ``S3Boto3StorageFile.buffer_size`` (via setting ``AWS_S3_FILE_BUFFER_SIZE``)
  at run-time rather than import-time. (`#930`_)
- Fix writing ``bytearray`` content (`#958`_, `#965`_)

Google Cloud
------------

- Add setting ``GS_QUERYSTRING_AUTH`` to avoid signing URLs. This is useful for buckets with a
  policy of Uniform public read (`#952`_)

Azure
-----

- Add ``AZURE_OBJECT_PARAMETERS`` and overridable ``AzureStorage.get_object_parameters`` to customize
  ``ContentSettings`` parameters for all keys and per-key respectively. (`#898`_)

.. _#382: https://github.com/jschneier/django-storages/issues/382
.. _#955: https://github.com/jschneier/django-storages/pull/955
.. _#930: https://github.com/jschneier/django-storages/pull/930
.. _#952: https://github.com/jschneier/django-storages/pull/952
.. _#898: https://github.com/jschneier/django-storages/pull/898
.. _#964: https://github.com/jschneier/django-storages/pull/964
.. _#958: https://github.com/jschneier/django-storages/issues/958
.. _#965: https://github.com/jschneier/django-storages/pull/965

1.10.1 (2020-09-13)
*******************

S3
--

- Restore ``AWS_DEFAULT_ACL`` handling. This setting is ignored if ``ACL`` is set in
  ``AWS_S3_OBJECT_PARAMETERS`` (`#934`_)

SFTP
----

- Fix using ``SFTP_STORAGE_HOST`` (`#926`_)

.. _#926: https://github.com/jschneier/django-storages/pull/926
.. _#934: https://github.com/jschneier/django-storages/pull/934

1.10 (2020-08-30)
*****************

General
-------

- **Breaking**: Removed support for end-of-life Python 2.7 and 3.4 (`#709`_)
- **Breaking**: Removed support for end-of-life Django 1.11 (`#891`_)
- Add support for Django 3.1 (`#916`_)
- Introduce a new ``BaseStorage`` class with a ``get_default_settings`` method and use
  it in ``S3Boto3Storage``, ``AzureStorage``, ``GoogleCloudStorage``, and ``SFTPStorage``. These backends
  now calculate their settings when instantiated, not imported. (`#524`_, `#852`_)

S3
--

- **Breaking**: Automatic bucket creation has been removed. Doing so encourages using overly broad credentials.
  As a result, support for the corresponding ``AWS_BUCKET_ACL`` and ``AWS_AUTO_CREATE_BUCKET`` settings have been removed. (`#636`_)
- **Breaking**: Support for the undocumented setting ``AWS_PRELOAD_METADATA`` has been removed (`#636`_)
- **Breaking**: The constructor kwarg ``acl`` is no longer accepted. Instead, use the ``ACL`` key in setting ``AWS_S3_OBJECT_PARAMETERS``
  (`#636`_)
- **Breaking**: The constructor kwarg ``bucket`` is no longer accepted. Instead, use ``bucket_name`` or the ``AWS_STORAGE_BUCKET_NAME``
  setting (`#636`_)
- **Breaking**: Support for setting ``AWS_REDUCED_REDUNDANCY`` has been removed. Replace with ``StorageClass=REDUCED_REDUNDANCY``
  in ``AWS_S3_OBJECT_PARAMETERS`` (`#636`_)
- **Breaking**: Support for setting ``AWS_S3_ENCRYPTION`` has been removed. Replace with ``ServerSideEncryption=AES256`` in ``AWS_S3_OBJECT_PARAMETERS`` (`#636`_)
- **Breaking**: Support for setting ``AWS_DEFAULT_ACL`` has been removed. Replace with ``ACL`` in ``AWS_S3_OBJECT_PARAMETERS`` (`#636`_)
- Add ``http_method`` parameter to ``.url`` method (`#854`_)
- Add support for signing Cloudfront URLs to the ``.url`` method. You must set ``AWS_CLOUDFRONT_KEY``,
  ``AWS_CLOUDFRONT_KEY_ID`` and install either `cryptography`_ or `rsa`_ (`#456`_, `#587`_). See the docs for more info.
  URLs will only be signed if ``AWS_QUERYSTRING_AUTH`` is set to ``True`` (`#885`_)

Google Cloud
------------

- **Breaking**: Automatic bucket creation has been removed. Doing so encourages using overly broad credentials.
  As a result, support for the corresponding ``GS_AUTO_CREATE_BUCKET`` and ``GS_AUTO_CREATE_ACL`` settings have been removed. (`#894`_)

Dropbox
-------

- Add ``DROPBOX_WRITE_MODE`` setting to control e.g. overwriting behavior. Check the docs
  for more info (`#873`_, `#138`_)

SFTP
----

- Remove exception swallowing during ssh connection (`#835`_, `#838`_)

FTP
---

- Add ``FTP_STORAGE_ENCODING`` setting to set the filesystem encoding  (`#803`_)
- Support multiple nested paths for files (`#886`_)

.. _cryptography: https://cryptography.io
.. _rsa: https://stuvel.eu/rsa
.. _#885: https://github.com/jschneier/django-storages/pull/885
.. _#894: https://github.com/jschneier/django-storages/pull/894
.. _#636: https://github.com/jschneier/django-storages/pull/636
.. _#709: https://github.com/jschneier/django-storages/pull/709
.. _#891: https://github.com/jschneier/django-storages/pull/891
.. _#916: https://github.com/jschneier/django-storages/pull/916
.. _#852: https://github.com/jschneier/django-storages/pull/852
.. _#873: https://github.com/jschneier/django-storages/pull/873
.. _#854: https://github.com/jschneier/django-storages/pull/854
.. _#138: https://github.com/jschneier/django-storages/issues/138
.. _#524: https://github.com/jschneier/django-storages/pull/524
.. _#835: https://github.com/jschneier/django-storages/issues/835
.. _#838: https://github.com/jschneier/django-storages/pull/838
.. _#803: https://github.com/jschneier/django-storages/pull/803
.. _#456: https://github.com/jschneier/django-storages/issues/456
.. _#587: https://github.com/jschneier/django-storages/pull/587
.. _#886: https://github.com/jschneier/django-storages/pull/886

1.9.1 (2020-02-03)
******************

S3
--

- Fix reading files with ``S3Boto3StorageFile`` (`#831`_, `#833`_)

.. _#831: https://github.com/jschneier/django-storages/issues/831
.. _#833: https://github.com/jschneier/django-storages/pull/833

1.9 (2020-02-02)
****************

General
-------

- **Breaking**: The long deprecated S3 backend based on ``boto`` has been removed. (`#825`_)
- Test against and support Python 3.8 (`#810`_)

S3
--

- **Deprecated**: Automatic bucket creation will be removed in version 1.10 (`#826`_)
- **Deprecated**: The undocumented ``AWS_PRELOAD_METADATA`` and associated functionality will
  be removed in version 1.10 (`#829`_)
- **Deprecated**: Support for ``AWS_REDUCED_REDUNDANCY`` will be removed in version 1.10
  Replace with ``StorageClass=REDUCED_REDUNDANCY`` in ``AWS_S3_OBJECT_PARAMETERS`` (`#829`_)
- **Deprecated**: Support for ``AWS_S3_ENCRYPTION`` will be removed in version 1.10 (`#829`_)
  Replace with ``ServerSideEncryption=AES256`` in ``AWS_S3_OBJECT_PARAMETERS``
- A custom ``ContentEncoding`` is no longer overwritten automatically (note that specifying
  one will disable automatic ``gzip``) (`#391`_, `#828`_).
- Add ``S3Boto3Storage.get_object_parameters``, an overridable method for customizing
  upload parameters on a per-object basis (`#819`_, `#828`_)
- Opening and closing a file in `w` mode without writing anything will now create an empty file
  in S3, this mimics the builtin ``open`` and Django's own ``FileSystemStorage`` (`#435`_, `#816`_)
- Fix reading a file in text mode (`#404`_, `#827`_)

Google Cloud
------------

- **Deprecated**: Automatic bucket creation will be removed in version 1.10 (`#826`_)

Dropbox
-------

- Fix crash on ``DropBoxStorage.listdir`` (`#762`_)
- Settings can now additionally be specified at the class level to ease subclassing (`#745`_)

Libcloud
--------

- Add support for Backblaze B2 to ``LibCloudStorage.url`` (`#807`_)

FTP
---

- Fix creating multiple intermediary directories on Windows (`#823`_, `#824`_)

.. _#825: https://github.com/jschneier/django-storages/pull/825
.. _#826: https://github.com/jschneier/django-storages/pull/826
.. _#829: https://github.com/jschneier/django-storages/pull/829
.. _#391: https://github.com/jschneier/django-storages/issues/391
.. _#828: https://github.com/jschneier/django-storages/pull/828
.. _#819: https://github.com/jschneier/django-storages/issues/819
.. _#810: https://github.com/jschneier/django-storages/pull/810
.. _#435: https://github.com/jschneier/django-storages/issues/435
.. _#816: https://github.com/jschneier/django-storages/pull/816
.. _#404: https://github.com/jschneier/django-storages/issues/404
.. _#827: https://github.com/jschneier/django-storages/pull/827
.. _#762: https://github.com/jschneier/django-storages/pull/762
.. _#745: https://github.com/jschneier/django-storages/pull/745
.. _#807: https://github.com/jschneier/django-storages/pull/807
.. _#823: https://github.com/jschneier/django-storages/issues/823
.. _#824: https://github.com/jschneier/django-storages/pull/824


1.8 (2019-11-20)
****************

General
-------
- Add support for Django 3.0 (`#759`_)
- Update license identifier to unambiguous ``BSD-3-Clause``

S3
--

- Include error message raised when missing library is imported (`#776`_, `#793`_)

Google
------

- **Breaking** The minimum supported version of ``google-cloud-storage`` is now ``1.15.0`` which enables...
- Add setting ``GS_CUSTOM_ENDPOINT`` to allow usage of custom domains (`#775`_, `#648`_)

Azure
-----

- Fix extra installation by pinning version to < 12 (`#785`_)
- Add support for setting ``AZURE_CACHE_CONTROL`` header (`#780`_, `#674`_)

.. _#759: https://github.com/jschneier/django-storages/pull/759
.. _#776: https://github.com/jschneier/django-storages/issues/776
.. _#793: https://github.com/jschneier/django-storages/pull/793
.. _#775: https://github.com/jschneier/django-storages/issues/775
.. _#648: https://github.com/jschneier/django-storages/pull/648
.. _#785: https://github.com/jschneier/django-storages/pull/785
.. _#780: https://github.com/jschneier/django-storages/pull/780
.. _#674: https://github.com/jschneier/django-storages/issues/674


1.7.2 (2019-09-10)
******************

S3
--

- Avoid misleading ``AWS_DEFAULT_ACL`` warning for insecure ``default_acl`` when
  overridden as a class variable (`#591`_)
- Propagate file deletion to cache when ``preload_metadata`` is ``True``,
  (not the default) (`#743`_, `#749`_)
- Fix exception raised on closed file (common if using ``ManifestFilesMixin`` or
  ``collectstatic``. (`#382`_, `#754`_)

Azure
-----

- Pare down the required packages in ``extra_requires`` when installing the ``azure`` extra to only
  ``azure-storage-blob`` (`#680`_, `#684`_)
- Fix compatibility with ``generate_blob_shared_access_signature`` updated signature (`#705`_, `#723`_)
- Fetching a file now uses the configured timeout rather than hardcoding one (`#727`_)
- Add support for configuring all blobservice options: ``AZURE_ENDPOINT_SUFFIX``,
  ``AZURE_CUSTOM_DOMAIN``, ``AZURE_CONNECTION_STRING``, ``AZURE_TOKEN_CREDENTIAL``.
  See the docs for more info. Huge thanks once again to @nitely. (`#750`_)
- Fix filename handling to not strip special characters (`#609`_, `#752`_)


Google Cloud
------------

- Set the file acl in the same call that uploads it (`#698`_)
- Reduce the number of queries and required permissions when ``GS_AUTO_CREATE_BUCKET`` is
  ``False`` (the default) (`#412`_, `#718`_)
- Set the ``predefined_acl`` when creating a ``GoogleCloudFile`` using ``.write``
  (`#640`_, `#756`_)
- Add ``GS_BLOB_CHUNK_SIZE`` setting to enable efficient uploading of large files (`#757`_)

Dropbox
-------

- Complete migration to v2 api with file fetching and metadata fixes (`#724`_)
- Add ``DROPBOX_TIMEOUT`` to configure client timeout defaulting to 100 seconds
  to match the underlying sdk. (`#419`_, `#747`_)

SFTP
----

- Fix reopening a file (`#746`_)

.. _#591: https://github.com/jschneier/django-storages/pull/591
.. _#680: https://github.com/jschneier/django-storages/issues/680
.. _#684: https://github.com/jschneier/django-storages/pull/684
.. _#698: https://github.com/jschneier/django-storages/pull/698
.. _#705: https://github.com/jschneier/django-storages/issues/705
.. _#723: https://github.com/jschneier/django-storages/pull/723
.. _#727: https://github.com/jschneier/django-storages/pull/727
.. _#746: https://github.com/jschneier/django-storages/pull/746
.. _#724: https://github.com/jschneier/django-storages/pull/724
.. _#412: https://github.com/jschneier/django-storages/pull/412
.. _#718: https://github.com/jschneier/django-storages/pull/718
.. _#743: https://github.com/jschneier/django-storages/issues/743
.. _#749: https://github.com/jschneier/django-storages/pull/749
.. _#750: https://github.com/jschneier/django-storages/pull/750
.. _#609: https://github.com/jschneier/django-storages/issues/609
.. _#752: https://github.com/jschneier/django-storages/pull/752
.. _#382: https://github.com/jschneier/django-storages/issues/382
.. _#754: https://github.com/jschneier/django-storages/pull/754
.. _#419: https://github.com/jschneier/django-storages/issues/419
.. _#747: https://github.com/jschneier/django-storages/pull/747
.. _#640: https://github.com/jschneier/django-storages/issues/640
.. _#756: https://github.com/jschneier/django-storages/pull/756
.. _#757: https://github.com/jschneier/django-storages/pull/757

1.7.1 (2018-09-06)
******************

- Fix off-by-1 error in ``get_available_name`` whenever ``file_overwrite`` or ``overwrite_files`` is ``True`` (`#588`_, `#589`_)
- Change ``S3Boto3Storage.listdir()`` to use ``list_objects`` instead of ``list_objects_v2`` to restore
  compatibility with services implementing the S3 protocol that do not yet support the new method (`#586`_, `#590`_)

.. _#588: https://github.com/jschneier/django-storages/issues/588
.. _#589: https://github.com/jschneier/django-storages/pull/589
.. _#586: https://github.com/jschneier/django-storages/issues/586
.. _#590: https://github.com/jschneier/django-storages/pull/590

1.7 (2018-09-03)
****************

**Security**

- The ``S3BotoStorage`` and ``S3Boto3Storage`` backends have an insecure
  default ACL of ``public-read``. It is recommended that all current users audit their bucket
  permissions.  Support has been added for setting ``AWS_DEFAULT_ACL = None`` and ``AWS_BUCKET_ACL =
  None`` which causes all created files to inherit the bucket's ACL (and created buckets to inherit the
  Amazon account's default ACL). This will become the default in version 1.10 (for ``S3Boto3Storage`` only
  since ``S3BotoStorage`` will be removed in version 1.9, see below). Additionally, a warning is now
  raised if ``AWS_DEFAULT_ACL`` or ``AWS_BUCKET_ACL`` is not explicitly set. (`#381`_, `#535`_, `#579`_)

**Breaking**

- The ``AzureStorage`` backend and documentation has been completely rewritten. It now
  depends on ``azure`` and ``azure-storage-blob`` and is *vastly* improved. Big thanks to @nitely and all
  other contributors along the way (`#565`_)
- The ``.url()`` method of ``GoogleCloudStorage`` has been completely reworked. Many use
  cases should require no changes and will experience a massive speedup. The ``.url()`` method no longer hits
  the network for public urls and generates signed urls (with a default of 1-day expiration, configurable
  via ``GS_EXPIRATION``) for non-public buckets.  Check out the docs for more information. (`#570`_)
- Various backends will now raise ``ImproperlyConfigured`` at runtime if their
  location (``GS_LOCATION``, ``AWS_LOCATION``) begins with a leading ``/`` rather than silently
  stripping it.  Verify yours does not. (`#520`_)
- The long deprecated ``GSBotoStorage`` backend is removed. (`#518`_)

**Deprecation**

- The insecure default of ``public-read`` for ``AWS_DEFAULT_ACL`` and
  ``AWS_BUCKET_ACL`` in ``S3Boto3Storage`` will change to inherit the bucket's setting in version 1.10 (`#579`_)
- The legacy ``S3BotoBackend`` is deprecated and will be removed in version 1.9.
  It is strongly recommended to move to the ``S3Boto3Storage`` backend for performance,
  stability and bugfix reasons. See the `boto migration docs`_ for step-by-step guidelines. (`#578`_, `#584`_)
- The long aliased arguments to ``S3Boto3Storage`` of ``acl`` and ``bucket`` are
  deprecated in favor of ``bucket_name`` and ``default_acl`` (`#516`_)
- The minimum required version of ``boto3`` will be increasing to ``1.4.4`` in
  the next major version of ``django-storages``. (`#583`_)

**Features**

- Add support for a file to inherit its bucket's ACL by setting ``AWS_DEFAULT_ACL = None`` (`#535`_)
- Add ``GS_CACHE_CONTROL`` setting for ``GoogleCloudStorage`` backend (`#411`_, `#505`_)
- Add documentation around using django-storages with Digital Ocean Spaces (`#521`_)
- Add support for Django 2.1 and Python 3.7 (`#530`_)
- Make ``S3Boto3Storage`` pickleable (`#551`_)
- Add automatic reconnection to ``SFTPStorage`` (`#563`_, `#564`_)
- Unconditionally set the security token in the boto backends (`b13efd`_)
- Improve efficiency of ``.listdir`` on ``S3Boto3Storage`` (`#352`_)
- Add ``AWS_S3_VERIFY`` to support custom certificates and disabling certificate verification
  to ``S3Boto3Storage`` (`#486`_, `#580`_)
- Add ``AWS_S3_PROXIES`` setting to ``S3Boto3Storage`` (`#583`_)
- Add a snazzy new logo. Big thanks to @reallinfo

**Bugfixes**

- Reset file read offset before passing to ``GoogleCloudStorage`` and ``AzureStorage`` (`#481`_, `#581`_, `#582`_)
- Fix various issues with multipart uploads in the S3 backends
  (`#169`_, `#160`_, `#364`_, `#449`_, `#504`_, `#506`_, `#546`_)
- Fix ``S3Boto3Storage`` to stream down large files (also disallow `r+w` mode) (`#383`_, `#548`_)
- Fix ``SFTPStorageFile`` to align with the core ``File`` abstraction (`#487`_, `#568`_)
- Catch ``IOError`` in ``SFTPStorage.delete`` (`#568`_)
- ``AzureStorage``, ``GoogleCloudStorage``, ``S3Boto3Storage`` and ``S3BotoStorage`` now
  respect ``max_length`` when ``file_overwrite = True`` (`#513`_, `#554`_)
- The S3 backends now consistently use ``compresslevel=9`` (the Python stdlib default)
  for gzipped content (`#572`_, `#576`_)
- Improve error message of ``S3Boto3Storage`` during an unexpected exception when automatically
  creating a bucket (`#574`_, `#577`_)

.. _#381: https://github.com/jschneier/django-storages/issues/381
.. _#535: https://github.com/jschneier/django-storages/pull/535
.. _#579: https://github.com/jschneier/django-storages/pull/579
.. _#565: https://github.com/jschneier/django-storages/pull/565
.. _#520: https://github.com/jschneier/django-storages/pull/520
.. _#518: https://github.com/jschneier/django-storages/pull/518
.. _#516: https://github.com/jschneier/django-storages/pull/516
.. _#481: https://github.com/jschneier/django-storages/pull/481
.. _#581: https://github.com/jschneier/django-storages/pull/581
.. _#582: https://github.com/jschneier/django-storages/pull/582
.. _#411: https://github.com/jschneier/django-storages/issues/411
.. _#505: https://github.com/jschneier/django-storages/pull/505
.. _#521: https://github.com/jschneier/django-storages/pull/521
.. _#169: https://github.com/jschneier/django-storages/pull/169
.. _#160: https://github.com/jschneier/django-storages/issues/160
.. _#364: https://github.com/jschneier/django-storages/pull/364
.. _#449: https://github.com/jschneier/django-storages/issues/449
.. _#504: https://github.com/jschneier/django-storages/pull/504
.. _#530: https://github.com/jschneier/django-storages/pull/530
.. _#506: https://github.com/jschneier/django-storages/pull/506
.. _#546: https://github.com/jschneier/django-storages/pull/546
.. _#383: https://github.com/jschneier/django-storages/issues/383
.. _#548: https://github.com/jschneier/django-storages/pull/548
.. _b13efd: https://github.com/jschneier/django-storages/commit/b13efd92b3bf3e9967b8e7819224bfcf9abb977e
.. _#551: https://github.com/jschneier/django-storages/pull/551
.. _#563: https://github.com/jschneier/django-storages/issues/563
.. _#564: https://github.com/jschneier/django-storages/pull/564
.. _#487: https://github.com/jschneier/django-storages/issues/487
.. _#568: https://github.com/jschneier/django-storages/pull/568
.. _#513: https://github.com/jschneier/django-storages/issues/513
.. _#554: https://github.com/jschneier/django-storages/pull/554
.. _#570: https://github.com/jschneier/django-storages/pull/570
.. _#572: https://github.com/jschneier/django-storages/issues/572
.. _#576: https://github.com/jschneier/django-storages/pull/576
.. _#352: https://github.com/jschneier/django-storages/pull/352
.. _#574: https://github.com/jschneier/django-storages/issues/574
.. _#577: https://github.com/jschneier/django-storages/pull/577
.. _#486: https://github.com/jschneier/django-storages/pull/486
.. _#580: https://github.com/jschneier/django-storages/pull/580
.. _#583: https://github.com/jschneier/django-storages/pull/583
.. _boto migration docs:  https://django-storages.readthedocs.io/en/latest/backends/amazon-S3.html#migrating-boto-to-boto3
.. _#578: https://github.com/jschneier/django-storages/pull/578
.. _#584: https://github.com/jschneier/django-storages/pull/584

1.6.6 (2018-03-26)
******************

* You can now specify the backend you are using to install the necessary dependencies using
  ``extra_requires``. For example ``pip install django-storages[boto3]`` (`#417`_)
* Add additional content-type detection fallbacks (`#406`_, `#407`_)
* Add ``GS_LOCATION`` setting to specify subdirectory for ``GoogleCloudStorage`` (`#355`_)
* Add support for uploading large files to ``DropBoxStorage``, fix saving files (`#379`_, `#378`_, `#301`_)
* Drop support for Django 1.8 and Django 1.10 (and hence Python 3.3) (`#438`_)
* Implement ``get_created_time`` for ``GoogleCloudStorage`` (`#464`_)

.. _#417: https://github.com/jschneier/django-storages/pull/417
.. _#407: https://github.com/jschneier/django-storages/pull/407
.. _#406: https://github.com/jschneier/django-storages/issues/406
.. _#355: https://github.com/jschneier/django-storages/pull/355
.. _#379: https://github.com/jschneier/django-storages/pull/379
.. _#378: https://github.com/jschneier/django-storages/issues/378
.. _#301: https://github.com/jschneier/django-storages/issues/301
.. _#438: https://github.com/jschneier/django-storages/issues/438
.. _#464: https://github.com/jschneier/django-storages/pull/464

1.6.5 (2017-08-01)
******************

* Fix Django 1.11 regression with gzipped content being saved twice
  resulting in empty files (`#367`_, `#371`_, `#373`_)
* Fix the ``mtime`` when gzipping content on ``S3Boto3Storage`` (`#374`_)

.. _#367: https://github.com/jschneier/django-storages/issues/367
.. _#371: https://github.com/jschneier/django-storages/pull/371
.. _#373: https://github.com/jschneier/django-storages/pull/373
.. _#374: https://github.com/jschneier/django-storages/pull/374

1.6.4 (2017-07-27)
******************

* Files uploaded with ``GoogleCloudStorage`` will now set their appropriate mimetype (`#320`_)
* Fix ``DropBoxStorage.url`` to work. (`#357`_)
* Fix ``S3Boto3Storage`` when ``AWS_PRELOAD_METADATA = True`` (`#366`_)
* Fix ``S3Boto3Storage`` uploading file-like objects without names (`#195`_, `#368`_)
* ``S3Boto3Storage`` is now threadsafe - a separate session is created on a
  per-thread basis (`#268`_, `#358`_)

.. _#320: https://github.com/jschneier/django-storages/pull/320
.. _#357: https://github.com/jschneier/django-storages/pull/357
.. _#366: https://github.com/jschneier/django-storages/pull/366
.. _#195: https://github.com/jschneier/django-storages/pull/195
.. _#368: https://github.com/jschneier/django-storages/pull/368
.. _#268: https://github.com/jschneier/django-storages/issues/268
.. _#358: https://github.com/jschneier/django-storages/pull/358

1.6.3 (2017-06-23)
******************

* Revert default ``AWS_S3_SIGNATURE_VERSION`` to V2 to restore backwards
  compatibility in ``S3Boto3``. It's recommended that all new projects set
  this to be ``'s3v4'``. (`#344`_)

.. _#344: https://github.com/jschneier/django-storages/pull/344

1.6.2 (2017-06-22)
******************

* Fix regression in ``safe_join()`` to handle a trailing slash in an
  intermediate path. (`#341`_)
* Fix regression in ``gs.GSBotoStorage`` getting an unexpected kwarg.
  (`#342`_)

.. _#341: https://github.com/jschneier/django-storages/pull/341
.. _#342: https://github.com/jschneier/django-storages/pull/342

1.6.1 (2017-06-22)
******************

* Drop support for Django 1.9 (`e89db45`_)
* Fix regression in ``safe_join()`` to allow joining a base path with an empty
  string. (`#336`_)

.. _e89db45: https://github.com/jschneier/django-storages/commit/e89db451d7e617638b5991e31df4c8de196546a6
.. _#336: https://github.com/jschneier/django-storages/pull/336

1.6 (2017-06-21)
******************

* **Breaking:** Remove backends deprecated in v1.5.1 (`#280`_)
* **Breaking:** ``DropBoxStorage`` has been upgrade to support v2 of the API, v1 will be shut off at the
  end of the month - upgrading is recommended (`#273`_)
* **Breaking:** The ``SFTPStorage`` backend now checks for the existence of the fallback ``~/.ssh/known_hosts``
  before attempting to load it.  If you had previously been passing in a path to a non-existent file it will no longer
  attempt to load the fallback. (`#118`_, `#325`_)
* **Breaking:** The default version value for ``AWS_S3_SIGNATURE_VERSION`` is now ``'s3v4'``. No changes should
  be required (`#335`_)
* **Deprecation:** The undocumented ``gs.GSBotoStorage`` backend. See the new ``gcloud.GoogleCloudStorage``
  or ``apache_libcloud.LibCloudStorage`` backends instead. (`#236`_)
* Add a new backend, ``gcloud.GoogleCloudStorage`` based on the ``google-cloud`` bindings. (`#236`_)
* Pass in the location constraint when auto creating a bucket in ``S3Boto3Storage`` (`#257`_, `#258`_)
* Add support for reading ``AWS_SESSION_TOKEN`` and ``AWS_SECURITY_TOKEN`` from the environment
  to ``S3Boto3Storage`` and ``S3BotoStorage``. (`#283`_)
* Fix Boto3 non-ascii filenames on Python 2.7 (`#216`_, `#217`_)
* Fix ``collectstatic`` timezone handling in and add ``get_modified_time`` to ``S3BotoStorage`` (`#290`_)
* Add support for Django 1.11 (`#295`_)
* Add ``project`` keyword support to GCS in ``LibCloudStorage`` backend (`#269`_)
* Files that have a guessable encoding (e.g. gzip or compress) will be uploaded with that Content-Encoding in
  the ``s3boto3`` backend (`#263`_, `#264`_)
* The Dropbox backend now properly translates backslashes in Windows paths into forward slashes (`e52a127`_)
* The S3 backends now permit colons in the keys (`#248`_, `#322`_)

.. _#217: https://github.com/jschneier/django-storages/pull/217
.. _#273: https://github.com/jschneier/django-storages/pull/273
.. _#216: https://github.com/jschneier/django-storages/issues/216
.. _#283: https://github.com/jschneier/django-storages/pull/283
.. _#280: https://github.com/jschneier/django-storages/pull/280
.. _#257: https://github.com/jschneier/django-storages/issues/257
.. _#258: https://github.com/jschneier/django-storages/pull/258
.. _#290: https://github.com/jschneier/django-storages/pull/290
.. _#295: https://github.com/jschneier/django-storages/pull/295
.. _#269: https://github.com/jschneier/django-storages/pull/269
.. _#263: https://github.com/jschneier/django-storages/issues/263
.. _#264: https://github.com/jschneier/django-storages/pull/264
.. _e52a127: https://github.com/jschneier/django-storages/commit/e52a127523fdd5be50bb670ccad566c5d527f3d1
.. _#236: https://github.com/jschneier/django-storages/pull/236
.. _#118: https://github.com/jschneier/django-storages/issues/118
.. _#325: https://github.com/jschneier/django-storages/pull/325
.. _#248: https://github.com/jschneier/django-storages/issues/248
.. _#322: https://github.com/jschneier/django-storages/pull/322
.. _#335: https://github.com/jschneier/django-storages/pull/335

1.5.2 (2017-01-13)
******************

* Actually use ``SFTP_STORAGE_HOST`` in ``SFTPStorage`` backend (`#204`_)
* Fix ``S3Boto3Storage`` to avoid race conditions in a multi-threaded WSGI environment (`#238`_)
* Fix trying to localize a naive datetime when ``settings.USE_TZ`` is ``False`` in ``S3Boto3Storage.modified_time``.
  (`#235`_, `#234`_)
* Fix automatic bucket creation in ``S3Boto3Storage`` when ``AWS_AUTO_CREATE_BUCKET`` is ``True`` (`#196`_)
* Improve the documentation for the S3 backends

.. _#204: https://github.com/jschneier/django-storages/pull/204
.. _#238: https://github.com/jschneier/django-storages/pull/238
.. _#234: https://github.com/jschneier/django-storages/issues/234
.. _#235: https://github.com/jschneier/django-storages/pull/235
.. _#196: https://github.com/jschneier/django-storages/pull/196

1.5.1 (2016-09-13)
******************

* **Breaking:** Drop support for Django 1.7 (`#185`_)
* **Deprecation:** hashpath, image, overwrite, mogile, symlinkorcopy, database, mogile, couchdb.
  See (`#202`_) to discuss maintenance going forward
* Use a fixed ``mtime`` argument for ``GzipFile`` in ``S3BotoStorage`` and ``S3Boto3Storage`` to ensure
  a stable output for gzipped files
* Use ``.putfileobj`` instead of ``.put`` in ``S3Boto3Storage`` to use the transfer manager,
  allowing files greater than 5GB to be put on S3 (`#194`_ , `#201`_)
* Update ``S3Boto3Storage`` for Django 1.10 (`#181`_) (``get_modified_time`` and ``get_accessed_time``)
* Fix bad kwarg name in ``S3Boto3Storage`` when `AWS_PRELOAD_METADATA` is `True` (`#189`_, `#190`_)

.. _#202: https://github.com/jschneier/django-storages/issues/202
.. _#201: https://github.com/jschneier/django-storages/pull/201
.. _#194: https://github.com/jschneier/django-storages/issues/194
.. _#190: https://github.com/jschneier/django-storages/pull/190
.. _#189: https://github.com/jschneier/django-storages/issues/189
.. _#185: https://github.com/jschneier/django-storages/pull/185
.. _#181: https://github.com/jschneier/django-storages/pull/181

1.5.0 (2016-08-02)
******************

* Add new backend ``S3Boto3Storage`` (`#179`_)
* Add a `strict` option to `utils.setting` (`#176`_)
* Tests, documentation, fixing ``.close`` for ``SFTPStorage`` (`#177`_)
* Tests, documentation, add `.readlines` for ``FTPStorage`` (`#175`_)
* Tests and documentation for ``DropBoxStorage`` (`#174`_)
* Fix ``MANIFEST.in`` to not ship ``.pyc`` files. (`#145`_)
* Enable CI testing of Python 3.5 and fix test failure from api change (`#171`_)

.. _#145: https://github.com/jschneier/django-storages/pull/145
.. _#171: https://github.com/jschneier/django-storages/pull/171
.. _#174: https://github.com/jschneier/django-storages/pull/174
.. _#175: https://github.com/jschneier/django-storages/pull/175
.. _#177: https://github.com/jschneier/django-storages/pull/177
.. _#176: https://github.com/jschneier/django-storages/pull/176
.. _#179: https://github.com/jschneier/django-storages/pull/179

1.4.1 (2016-04-07)
******************

* Files that have a guessable encoding (e.g. gzip or compress) will be uploaded with that Content-Encoding
  in the ``s3boto`` backend. Compressable types such as ``application/javascript`` will still be gzipped.
  PR `#122`_
* Fix ``DropBoxStorage.exists`` check and add ``DropBoxStorage.url`` (`#127`_)
* Add ``GS_HOST`` setting (with a default of ``GSConnection.DefaultHost``) to fix ``GSBotoStorage``.
  (`#124`_, `#125`_)

.. _#122: https://github.com/jschneier/django-storages/pull/122
.. _#127: https://github.com/jschneier/django-storages/pull/127
.. _#124: https://github.com/jschneier/django-storages/issues/124
.. _#125: https://github.com/jschneier/django-storages/pull/125

1.4 (2016-02-07)
****************

* This package is now released on PyPI as `django-storages`. Please update your requirements files to
  `django-storages==1.4`.

1.3.2 (2016-01-26)
******************

* Fix memory leak from not closing underlying temp file in ``s3boto`` backend (`#106`_)
* Allow easily specifying a custom expiry time when generating a url for ``S3BotoStorage`` (`#96`_)
* Check for bucket existence when the empty path ('') is passed to ``storage.exists`` in ``S3BotoStorage`` -
  this prevents a crash when running ``collectstatic -c`` on Django 1.9.1 (`#112`_) fixed in `#116`_

.. _#106: https://github.com/jschneier/django-storages/pull/106
.. _#96: https://github.com/jschneier/django-storages/pull/96
.. _#112: https://github.com/jschneier/django-storages/issues/112
.. _#116: https://github.com/jschneier/django-storages/pull/116


1.3.1 (2016-01-12)
******************

* A few Azure Storage fixes [pass the content-type to Azure, handle chunked content, fix ``url``] (`#45`__)
* Add support for a Dropbox (``dropbox``) storage backend
* Various fixes to the ``apache_libcloud`` backend [return the number of bytes asked for by ``.read``, make ``.name`` non-private, don't
  initialize to an empty ``BytesIO`` object] (`#55`_)
* Fix multi-part uploads in ``s3boto`` backend not respecting ``AWS_S3_ENCRYPTION`` (`#94`_)
* Automatically gzip svg files (`#100`_)

.. __: https://github.com/jschneier/django-storages/pull/45
.. _#76: https://github.com/jschneier/django-storages/pull/76
.. _#55: https://github.com/jschneier/django-storages/pull/55
.. _#94: https://github.com/jschneier/django-storages/pull/94
.. _#100: https://github.com/jschneier/django-storages/pull/100


1.3 (2015-08-14)
****************

* **Breaking:** Drop Support for Django 1.5 and Python 2.6
* **Breaking:** Remove previously deprecated mongodb backend
* **Breaking:** Remove previously deprecated ``parse_ts_extended`` from s3boto storage
* Add support for Django 1.8+ (`#36`__)
* Add ``AWS_S3_PROXY_HOST`` and ``AWS_S3_PROXY_PORT`` settings for s3boto backend (`#41`_)
* Fix Python3K compat issue in apache_libcloud (`#52`_)
* Fix Google Storage backend not respecting ``GS_IS_GZIPPED`` setting (`#51`__, `#60`_)
* Rename FTP ``_name`` attribute to ``name`` which is what the Django ``File`` api is expecting (`#70`_)
* Put ``StorageMixin`` first in inheritance to maintain backwards compat with older versions of Django (`#63`_)

.. __: https://github.com/jschneier/django-storages/pull/36
.. _#41: https://github.com/jschneier/django-storages/pull/41
.. _#52: https://github.com/jschneier/django-storages/issues/52
.. __: https://github.com/jschneier/django-storages/pull/51
.. _#60: https://github.com/jschneier/django-storages/pull/60
.. _#70: https://github.com/jschneier/django-storages/pull/70
.. _#63: https://github.com/jschneier/django-storages/pull/63


1.2.3 (2015-03-14)
******************

* Variety of FTP backend fixes (fix ``exists``, add ``modified_time``, remove call to non-existent function) (`#26`_)
* Apparently the year changed to 2015

.. _#26: https://github.com/jschneier/django-storages/pull/26


1.2.2 (2015-01-28)
******************

* Remove always show all warnings filter (`#21`_)
* Release package as a wheel
* Avoid resource warning during install (`#20`__)
* Made ``S3BotoStorage`` deconstructible (previously only ``S3BotoStorageFile`` was deconstructible) (`#19`_)

.. _#21: https://github.com/jschneier/django-storages/pull/21
.. __: https://github.com/jschneier/django-storages/issues/20
.. _#19: https://github.com/jschneier/django-storages/pull/19


1.2.1 (2014-12-31)
******************

* **Deprecation:** Issue warning about ``parse_ts_extended``
* **Deprecation:** mongodb backend - django-mongodb-engine now ships its own storage backend
* Fix ``storage.modified_time`` crashing on new files when ``AWS_PRELOAD_METADATA=True`` (`#11`_, `#12`__, `#14`_)

.. _#11: https://github.com/jschneier/django-storages/pull/11
__ https://github.com/jschneier/django-storages/issues/12
.. _#14: https://github.com/jschneier/django-storages/pull/14


1.2 (2014-12-14)
****************

* **Breaking:** Remove legacy S3 storage (`#1`_)
* **Breaking:** Remove mosso files backend (`#2`_)
* Add text/javascript mimetype to S3BotoStorage gzip allowed defaults
* Add support for Django 1.7 migrations in S3BotoStorage and ApacheLibCloudStorage (`#5`_, `#8`_)
* Python3K (3.3+) now available for S3Boto backend (`#4`_)

.. _#8: https://github.com/jschneier/django-storages/pull/8
.. _#5: https://github.com/jschneier/django-storages/pull/5
.. _#4: https://github.com/jschneier/django-storages/pull/4
.. _#1: https://github.com/jschneier/django-storages/issues/1
.. _#2: https://github.com/jschneier/django-storages/issues/2


**NOTE**: Version 1.1.9 is the first release of django-storages after the fork.
It represents the current (2014-12-08) state of the original django-storages in
master with no additional changes. This is the first release of the code base
since March 2013.

1.1.9 (2014-12-08)
******************

* Fix syntax for Python3 with pull-request `#91`_
* Support pushing content type from File object to GridFS with pull-request `#90`_
* Support passing a region to the libcloud driver with pull-request `#86`_
* Handle trailing slash paths fixes `#188`_ fixed by pull-request `#85`_
* Use a SpooledTemporaryFile to conserve memory in S3BotoFile pull-request `#69`_
* Guess content-type for S3BotoStorageFile the same way that _save() in S3BotoStorage does
* Pass headers and response_headers through from url to generate_url in S3BotoStorage pull-request `#65`_
* Added AWS_S3_HOST, AWS_S3_PORT and AWS_S3_USE_SSL settings to specify host, port and is_secure in pull-request `#66`_

.. _#91: https://bitbucket.org/david/django-storages/pull-request/91/
.. _#90: https://bitbucket.org/david/django-storages/pull-request/90/
.. _#86: https://bitbucket.org/david/django-storages/pull-request/86/
.. _#188: https://bitbucket.org/david/django-storages/issue/188/s3boto-_clean_name-is-broken-and-leads-to
.. _#85: https://bitbucket.org/david/django-storages/pull-request/85/
.. _#69: https://bitbucket.org/david/django-storages/pull-request/69/
.. _#66: https://bitbucket.org/david/django-storages/pull-request/66/
.. _#65: https://bitbucket.org/david/django-storages/pull-request/65/


**Everything Below Here Was Previously Released on PyPI under django-storages**


1.1.8 (2013-03-31)
******************

* Fixes `#156`_ regarding date parsing, ValueError when running collectstatic
* Proper handling of boto dev version parsing
* Made SFTP URLs accessible, now uses settings.MEDIA_URL instead of sftp://

.. _#156: https://bitbucket.org/david/django-storages/issue/156/s3boto-backend-valueerror-time-data-thu-07

1.1.7 (2013-03-20)
******************

* Listing of huge buckets on S3 is now prevented by using the prefix argument to boto's list() method
* Initial support for Windows Azure Storage
* Switched to useing boto's parse_ts date parser getting last modified info when using S3boto backend
* Fixed key handling in S3boto and Google Storage backends
* Account for lack of multipart upload in Google Storage backend
* Fixed seek() issue when using AWS_IS_GZIPPED by darkness51 with pull-request `#50`_
* Improvements to S3BotoStorage and GSBotoStorage

.. _#50: https://bitbucket.org/david/django-storages/pull-request/50/

1.1.6 (2013-01-06)
******************

* Merged many changes from Jannis Leidel (mostly regarding gzipping)
* Fixed tests by Ian Lewis
* Added support for Google Cloud Storage backend by Jannis Leidel
* Updated license file by Dan Loewenherz, fixes `#133`_ with pull-request `#44`_
* Set Content-Type header for use in upload_part_from_file by Gerardo Curiel
* Pass the rewind parameter to Boto's set_contents_from_file method by Jannis Leidel with pull-request `#45`_
* Fix for FTPStorageFile close() method by Mathieu Comandon with pull-request `#43`_
* Minor refactoring by Oktay Sancak with pull-request `#48`_
* Ungzip on download based on Content-Encoding by Gavin Wahl with pull-request `#46`_
* Add support for S3 server-side encryption by Tobias McNulty with pull-request `#17`_
* Add an optional setting to the boto storage to produce protocol-relative URLs, fixes `#105`_

.. _#133: https://bitbucket.org/david/django-storages/issue/133/license-file-refers-to-incorrect-project
.. _#44: https://bitbucket.org/david/django-storages/pull-request/44/
.. _#45: https://bitbucket.org/david/django-storages/pull-request/45/
.. _#43: https://bitbucket.org/david/django-storages/pull-request/43/
.. _#48: https://bitbucket.org/david/django-storages/pull-request/48/
.. _#46: https://bitbucket.org/david/django-storages/pull-request/46/
.. _#17: https://bitbucket.org/david/django-storages/pull-request/17/
.. _#105: https://bitbucket.org/david/django-storages/issue/105/add-option-to-produce-protocol-relative


1.1.5 (2012-07-18)
******************

* Merged pull request `#36`_ from freakboy3742 Keith-Magee, improvements to Apache Libcloud backend and docs
* Merged pull request `#35`_ from atodorov, allows more granular S3 access settings
* Add support for SSL in Rackspace Cloudfiles backend
* Fixed the listdir() method in s3boto backend, fixes `#57`_
* Added base url tests for safe_join in s3boto backend
* Merged pull request `#20`_ from alanjds, fixed SuspiciousOperation warning if AWS_LOCATION ends with '/'
* Added FILE_BUFFER_SIZE setting to s3boto backend
* Merged pull request `#30`_ from pendletongp, resolves `#108`_, `#109`_ and `#110`_
* Updated the modified_time() method so that it doesn't require dateutil. fixes `#111`_
* Merged pull request `#16`_ from chamal, adds Apache Libcloud backend
* When preloading the S3 metadata make sure we reset the files key during saving to prevent stale metadata
* Merged pull request `#24`_ from tobias.mcnulty, fixes bug where s3boto backend returns modified_time in wrong time zone
* Fixed HashPathStorage.location to no longer use settings.MEDIA_ROOT
* Remove download_url from setup file so PyPI dist is used

.. _#36: https://bitbucket.org/david/django-storages/pull-request/36/
.. _#35: https://bitbucket.org/david/django-storages/pull-request/35/
.. _#57: https://bitbucket.org/david/django-storages/issue/57
.. _#20: https://bitbucket.org/david/django-storages/pull-request/20/
.. _#30: https://bitbucket.org/david/django-storages/pull-request/30/
.. _#108: https://bitbucket.org/david/django-storages/issue/108
.. _#109: https://bitbucket.org/david/django-storages/issue/109
.. _#110: https://bitbucket.org/david/django-storages/issue/110
.. _#111: https://bitbucket.org/david/django-storages/issue/111
.. _#16: https://bitbucket.org/david/django-storages/pull-request/16/
.. _#24: https://bitbucket.org/david/django-storages/pull-request/24/

1.1.4 (2012-01-06)
******************

* Added PendingDeprecationWarning for mosso backend
* Merged pull request `#13`_ from marcoala, adds ``SFTP_KNOWN_HOST_FILE`` setting to SFTP storage backend
* Merged pull request `#12`_ from ryankask, fixes HashPathStorage tests that delete remote media
* Merged pull request `#10`_ from key, adds support for django-mongodb-engine 0.4.0 or later, fixes GridFS file deletion bug
* Fixed S3BotoStorage performance problem calling modified_time()
* Added deprecation warning for s3 backend, refs `#40`_
* Fixed CLOUDFILES_CONNECTION_KWARGS import error, fixes `#78`_
* Switched to sphinx documentation, set official docs up on https://django-storages.readthedocs.io/
* HashPathStorage uses self.exists now, fixes `#83`_

.. _#13: https://bitbucket.org/david/django-storages/pull-request/13/a-version-of-sftp-storage-that-allows-you
.. _#12: https://bitbucket.org/david/django-storages/pull-request/12/hashpathstorage-tests-deleted-my-projects
.. _#10: https://bitbucket.org/david/django-storages/pull-request/10/support-django-mongodb-engine-040
.. _#40: https://bitbucket.org/david/django-storages/issue/40/deprecate-s3py-backend
.. _#78: https://bitbucket.org/david/django-storages/issue/78/import-error
.. _#83: https://bitbucket.org/david/django-storages/issue/6/symlinkorcopystorage-new-custom-storage

1.1.3 (2011-08-15)
******************

* Created this lovely change log
* Fixed `#89`_: broken StringIO import in CloudFiles backend
* Merged `pull request #5`_: HashPathStorage path bug

.. _#89: https://bitbucket.org/david/django-storages/issue/89/112-broke-the-mosso-backend
.. _pull request #5: https://bitbucket.org/david/django-storages/pull-request/5/fixed-path-bug-and-added-testcase-for
