# Egoistat

Webservice and application providing social popularity statistics 
for your website.

## Motivation

Nothing fancy, just wanted to have simple and neat API to get all the 
statistics I want. I'm also kinda pedantic and wanted to style social 
buttons whatever I like in an easy way. I hope that this app will be
also simple for you and you'll enjoy using it.

Btw, this application is proudly written in Go language. It turned out
to be a translated version of similar webservice I wrote in Ruby. 
However, unlike the Ruby ones this is **fully parallel** and at the end
**aprox. 10 times faster** than original one (benchmarks don't lie). 
Check out my [blog post](http://areyoufuckingcoding.me/2012/08/14/parallelism-for-the-win/) 
to get more details.

## Getting started

This is standard Go web application. Just clone the repo and do the standard
steps.

    $ git clone git://github.com/nu7hatch/egoistat.git
    $ cd egoistat
    $ go get . && go build ./...
    $ go test ./...

Now run the server with:

    $ ./egoistat ":8080"

Go to `http://localhost:8080` and enjoy.

## API Usage

Egoistat provides public API which can be queried in two ways. You can 
perform standard HTTP query to get social networks' points in JSON format:

    $ curl -H 'Accept: application/json' http://egoistat.com/api/v1/stat.json?url=PAGE_URL&n=NETWORKS

`PAGE_URL` must be full URL with scheme specified, eg. http://egoistat.net/.
Note, that the most correct results for the domain comes when trailing
slash is in the address.

`NETWORKS` gets comma separated list of social networks to get points from. 
Currently available networks are: `facebook`, `twitter`, `plusone`, `reddit`, 
`hackernews` and `github`.

You can also request a script ready to use on your website, so that no backend 
calls will be required:

    <script src="//egoistat.com/api/v1/stat.js?url=PAGE_URL&n=NETWORKS&cb=CALLBACK"></script>

This script defines the egoistat global variable - it responds to `points(sn)` function which
return points count for specified social network `sn`.

It is also possible to specify `CALLBACK` which is going to be executed after
script gets loaded.

## Deployment

This app is heroku ready, so if you want to deply it there it's uber simple.
Just run:

    $ make deploy

This target makes sure that assets are compiled and pushes everything to
heroku's remote. 

## Development

Frontend of the application is written in HTML5 + Backbone.js. Source
assets can be found in `assets/` directory. Files in `public/js` and
`public/css` are generated and should not be edited.

In development you should use `juicer` and `guard` ruby gems. Install
it with command (you must have ruby 1.9 installed):

    $ make gems

Now you're able to use assets compression and bundling:

    $ make scripts
    $ make styles

Specifying `DEV` switch you can turn minifying on and off. For example
the following command will only merge scripts, without minifying.

    $ make scripts DEV=1

All scripts and styles can be merged with one command:

    $ make assets

To speed up development use `guard`. This command will run watcher
on `assets/` directory: 

    $ make guard

Every time source file changes it will rebuild assets and reload 
your browser (if it has [LiveReload](http://livereload.com/) addon
enabled).

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Added some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## Copying

Copyright (c) 2012 by Chris Kowalik a.k.a. nu7hatch

Released under AGPLv3 license. Check LICENSE for details.
