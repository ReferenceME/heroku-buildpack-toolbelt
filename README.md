Heroku buildpack: Heroku Toolbelt
=========================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) that
allows one to run Heroku Toolbelt in a dyno alongside application code.

This is not a replacement for the [Heroku API](https://devcenter.heroku.com/articles/platform-api-reference#overview) or various clients like [v3 Ruby](https://github.com/heroku/platform-api), [v2 Ruby](https://github.com/heroku/heroku.rb), [node](https://www.npmjs.org/package/heroku-client) or [python](https://github.com/heroku/heroku.py). Some private APIs like `pgbackups` do require the buildpack, so this exists.

It is meant to be used in conjunction with at least the
[minimal ruby](https://github.com/dpiddy/heroku-buildpack-ruby-minimal)


Usage
-----

Warning: The required environment variables **must be set** before running a deploy with the buildpack, otherwise the `.netrc` file will be malformed and any executable or library that relies on it won't work.

Example usage:

    $ heroku config:set HEROKU_TOOLBELT_API_EMAIL=hello@example.com -a my-app
    $ heroku config:set HEROKU_TOOLBELT_API_PASSWORD=`heroku auth:token` -a my-app
    

    $ heroku buildpacks:add https://github.com/ReferenceME/heroku-buildpack-toolbelt -a my-app


    $ heroku buildpacks -a my-app
    === my-app Buildpack URLs
    1. https://github.com/heroku/heroku-buildpack-ruby
    2. https://github.com/ReferenceME/heroku-buildpack-toolbelt


    $ git push heroku master


    $ heroku run 'vendor/heroku-toolbelt/bin/heroku auth:token' -a my-app
    Running `vendor/heroku-toolbelt/bin/heroku auth:token` attached to terminal... up, run.3706
    abc123-dce456-fgh789

Notes
------

Some PATH manipulation may be needed, expecially if you are using the
heroku-buildpack-ruby-minimal solely to provide a ruby execution environment
for the heroku cli gem. 
