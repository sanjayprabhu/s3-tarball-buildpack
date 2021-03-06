# S3 Tarball Buildpack

This is a [Heroku Buildpack](https://devcenter.heroku.com/articles/buildpacks)
that can download tarballs from private [Amazon S3](http://aws.amazon.com/s3/)
buckets. It gives you a way of deploying pre-built code to
[Heroku](http://www.heroku.com/) without making it publicly accessible.

## Usage

    $ heroku config:add BUILDPACK_URL=https://github.com/paulhammond/s3-tarball-buildpack.git

    $ cat .buildpack-s3-tarballs
    AWS_ACCESS_KEY_ID=AKIA0000000000000000
    AWS_SECRET_ACCESS_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
    s3://bucket/path/to/tarball.tgz
    s3://bucket/path/to/somethingelse.tgz

You probably want to use an [IAM key](http://aws.amazon.com/iam/) with limited
access. This code only requires `s3:GetObject` access to files.

If you don't want to check your IAM keys into revision control, you can store
them in Heroku's config system. Keys specified in the .buildpack-s3-tarballs
file have precedence over keys in the config system.

    $ heroku config:add BUILDPACK_URL=https://github.com/paulhammond/s3-tarball-buildpack.git
    $ heroku config:add AWS_ACCESS_KEY_ID=AKIA0000000000000000
    $ heroku config:add AWS_SECRET_ACCESS_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

    $ cat .buildpack-s3-tarballs
    s3://bucket/path/to/tarball.tgz

In most cases you'll use this buildpack in conjunction with other buildpacks
using [heroku-buildpack-multi](https://github.com/ddollar/heroku-buildpack-multi):

    $ heroku config:add BUILDPACK_URL=https://github.com/ddollar/heroku-buildpack-multi.git

    $ cat .buildpack-s3-tarballs
    AWS_ACCESS_KEY_ID=AKIA0000000000000000
    AWS_SECRET_ACCESS_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
    s3://bucket/path/to/tarball.tgz

    $ cat .buildpacks
    https://github.com/paulhammond/s3-tarball-buildpack.git
    https://github.com/ryandotsmith/null-buildpack.git

## See also

  * [heroku-buildpack-vendorbinaries](https://github.com/peterkeen/heroku-buildpack-vendorbinaries)
  * [s3simple](https://github.com/paulhammond/s3simple)
  * [Heroku Slug API](https://blog.heroku.com/archives/2013/12/20/programmatically_release_code_to_heroku_using_the_platform_api)

## Licence

MIT license, see LICENSE.txt for details.
