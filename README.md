## analytics.clevelandstatecc.edu

A project to publish website analytics for Cleveland State Community College. This is a fork of the public domain [analytics.usa.gov project](https://github.com/18F/analytics.usa.gov).

For a detailed description of how the site works, read [18F's blog post on analytics.usa.gov](https://18f.gsa.gov/2015/03/19/how-we-built-analytics-usa-gov/).

Other groups using this project for their analytics dashboards:
* https://analytics.usa.gov/
* http://analytics.phila.gov/
* https://bouldercolorado.gov/stats
* http://analytics.tdec.tn.gov/
  
[This blog post details their implementations and lessons learned](https://18f.gsa.gov/2016/01/05/tips-for-adapting-analytics-usa-gov/).  

### Setup

Ths app uses [Jekyll](http://jekyllrb.com) to build the site, and [Sass](http://sass-lang.com/), [Bourbon](http://bourbon.io), and [Neat](http://neat.bourbon.io) for CSS.

Install them all:

```bash
bundle install
```

[`analytics-reporter`](https://github.com/18F/analytics-reporter) is the code that powers the analytics dashboard.
Please clone the `analytics-reporter` next to a local copy of this github repository.

### Developing locally

Run Jekyll with development settings:

```bash
make dev
```

(This runs `bundle exec jekyll serve --watch --config _.yml,_development.yml`.)

Sass can watch the .scss source files for changes, and build the .css files automatically:

```bash
make watch
```

To compile the Sass stylesheets once, run `make clean all`, or `make -B` to compile even if the .css file already exists.

### Developing with local data

The development settings assume data is available at `http://localhost:4000`.

### Developing with real live data from `analytics-reporter`

If also working off of local data, e.g. using `analytics-reporter`, you will need to make the data available over HTTP _and_ through CORS.

Various tools can do this. This project recommends using the Node module `serve`:

```bash
npm install -g serve
```

Generate data to a directory:

```
analytics --output [dir]
```

Then run `serve` from the output directory:

```bash
serve --cors
```

The data will be available at `http://localhost:3000` over CORS, with no path prefix. For example, device data will be at `http://localhost:3000/devices.json`.


### Deploying the app to production

In production, the site's base URL is set to `https://analytics.usa.gov` and the data's base URL is set to `https://analytics.usa.gov/data/live`.

To deploy this app to `analytics.usa.gov`, you will need authorized access to 18F's Amazon S3 bucket for the project.

To deploy the site using `s3cmd`, production settings, and a **5 minute cache time**, run:

```bash
make deploy
```

**Use the full command above.** The full command ensures that the build completes successfully, with production settings, _before_ triggering an upload to the production bucket.

### Public domain

This project is in the worldwide [public domain](LICENSE.md). As stated in [CONTRIBUTING](CONTRIBUTING.md):

> This project is in the public domain within the United States, and copyright and related rights in the work worldwide are waived through the [CC0 1.0 Universal public domain dedication](https://creativecommons.org/publicdomain/zero/1.0/).
>
> All contributions to this project will be released under the CC0 dedication. By submitting a pull request, you are agreeing to comply with this waiver of copyright interest.


