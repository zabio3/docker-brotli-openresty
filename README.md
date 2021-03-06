# docker-brotli-openresty

## Supported tags and respective `Dockerfile` links

The following "flavors" are built from source and are intended for more advanced and custom usage, caveat emptor:

- [`xenial`, (*xenial/Dockerfile*)](https://github.com/openresty/docker-openresty/blob/master/xenial/Dockerfile)

Starting with `1.13.6.1`, releases are tagged with `<openresty-version>-<image-version>-<flavor>`.  The latest `image-version` will also be tagged `<openresty-version>-<flavor>`.   The HEAD of the master branch is also labeled plainly as `<flavor>`.  The builds are managed by [Travis-CI](https://travis-ci.org/openresty/docker-openresty) and [Appveyor](https://ci.appveyor.com/project/openresty/docker-openresty) (for Windows images).

It is *highly recommended* that you use the upstream-based images for best support.  For best stability, pin your images to the full tag, for example `1.13.6.2-0-xenial`.

Description
===========

Docker is a container management platform.( Fork: docker-openrety)

OpenResty is a full-fledged web application server by bundling the standard nginx core,
lots of 3rd-party nginx modules, as well as most of their external dependencies.

From non-RPM/DEB flavors, the following modules are included by default, but one can easily increase or decrease that with [custom build options](#build-options) :

 * file-aio
 * http_addition_module
 * http_auth_request_module
 * http_dav_module
 * http_flv_module
 * http_geoip_module=dynamic
 * http_gunzip_module
 * http_gzip_static_module
 * http_image_filter_module=dynamic
 * http_mp4_module
 * http_random_index_module
 * http_realip_module
 * http_secure_link_module
 * http_slice_module
 * http_ssl_module
 * http_stub_status_module
 * http_sub_module
 * http_v2_module
 * http_xslt_module=dynamic
 * ipv6
 * mail
 * mail_ssl_module
 * md5-asm
 * pcre-jit
 * sha1-asm
 * stream
 * stream_ssl_module
 * threads
 * **ngx_brotli (New addition)**


Usage
=====

If you are happy with the build defaults, then you can use the openresty image from the [Docker Hub](https://hub.docker.com/r/openresty/openresty/).  The image tags available there are listed at the top of this README.


Building (from source)
======================

This Docker image can be built and customized by cloning the repo and running `docker build` with the desired Dockerfile:

```
git clone https://github.com/zabio3/docker-openresty.git
cd docker-openresty
docker build -t myopenresty -f xenial/Dockerfile .
docker run myopenresty
```

Dockerfiles are provided for the following base systems, selecting the Dockerfile path with `-f`:

 * [Ubuntu Xenial](https://github.com/openresty/docker-openresty/blob/master/xenial/Dockerfile) (`xenial/Dockerfile`)

We used to support more build flavors but have trimmed that down.  Older Dockerfiles are archived in the [`archive`](https://github.com/openresty/docker-openresty/tree/master/archive) folder.


The following are the available build-time options. They can be set using the `--build-arg` CLI argument, like so:

```
docker build --build-arg RESTY_J=4 -f xenial/Dockerfile .
```

| Key | Default | Description |
:----- | :-----: |:----------- |
|RESTY_IMAGE_BASE | "ubuntu" | The Debian Docker image base to build `FROM`. |
|RESTY_IMAGE_TAG  | "xenial" / "3.7" | The Debian or Alpine Docker image tag to build `FROM`. |
|RESTY_VERSION | 1.13.6.2 | The version of OpenResty to use. |
|RESTY_LUAROCKS_VERSION | 2.4.4 | The version of LuaRocks to use. |
|RESTY_OPENSSL_VERSION | 1.1.0h  / 1.0.2k | The version of OpenSSL to use. |
|RESTY_PCRE_VERSION | 8.42 | The version of PCRE to use. |
|RESTY_J | 1 | Sets the parallelism level (-jN) for the builds. |
|RESTY_CONFIG_OPTIONS | "--with-file-aio --with-http_addition_module --with-http_auth_request_module --with-http_dav_module --with-http_flv_module --with-http_geoip_module=dynamic --with-http_gunzip_module --with-http_gzip_static_module --with-http_image_filter_module=dynamic --with-http_mp4_module --with-http_perl_module=dynamic --with-http_random_index_module --with-http_realip_module --with-http_secure_link_module --with-http_slice_module --with-http_ssl_module --with-http_stub_status_module --with-http_sub_module --with-http_v2_module --with-http_xslt_module=dynamic --with-ipv6 --with-mail --with-mail_ssl_module --with-md5-asm --with-pcre-jit --with-sha1-asm --with-stream --with-stream_ssl_module --with-threads" | Options to pass to OpenResty's `./configure` script. |
|RESTY_CONFIG_OPTIONS_MORE | "" | More options to pass to OpenResty's `./configure` script. |
