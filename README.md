# my-blog

My personal blog.

## Build the page with the docker container Jekyll:3.8

Information found at [this DEV post](https://dev.to/michael/compile-a-jekyll-project-without-installing-jekyll-or-ruby-by-using-docker-4184.).

```
docker run --rm -it --volume="$PWD:/srv/jekyll" --volume="$PWD/vendor/bundle:/usr/local/bundle" --env JEKYLL_ENV=production jekyll/jekyll:3.8 jekyll build
```

If there is an error with this command about the service, start the daemon `systemctl start docker`.

What this command does is:

-    `--rm` automatically removes the container when it exits.
-    `--volume="$PWD:/srv/jekyll"` takes the current directory indicated by $PWD and map it to the directory at /srv/jekyll within the container so that it could build it.
-    `--volume="$PWD/vendor/bundle:/usr/local/bundle"` this option maps the contents of the current directory's /vendor/bundle and maps it to /usr/local/bundle. The reason for this option is so that gems could be cached and reused in future builds.
-    `--env JEKYLL_ENV=production` in various parts of my Jekyll project, I've designated for it to only render if it's for production. For example analytics shouldn't be muddied up by my local development. This sets the environment variable for JEKYLL_ENV to production.
-    `jekyll/jekyll:3.8` this tells it to use the jekyll:3.8 tagged version of the Jekyll container.
-    `jekyll build` runs the build command for Jekyll.

## Serve the page with the docker container

This serve the page in development mode at http://localhost:4000.

```
docker run --rm --volume="$PWD:/srv/jekyll" --volume="$PWD/vendor/bundle:/usr/local/bundle" --env JEKYLL_ENV=development -p 4000:4000 jekyll/jekyll:3.8 jekyll serve
```
