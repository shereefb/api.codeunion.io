# Code Union API

An HTTP API serving JSON data for Code Union resources.

## Installation

After cloning the repository, run

```shell-session
$ bundle install
$ rake db:setup
$ bundle exec foreman start
```

**Note**: See below if `bundle exec` gives you an error along the lines of

```text
Your Ruby version is 2.1.5, but your Gemfile specified 2.0.0
```

### Ruby Version

Heroku recommends we specify the version of Ruby to use in our
[Gemfile](Gemfile), which we do.  We read the version from an environment
variable named `CUSTOM_RUBY_VERSION`.  Otherwise, we use Heroku's
default Ruby version of `2.0.0`.

If you want to use a different version of Ruby locally, just set the
`CUSTOM_RUBY_VERSION` environment variable by adding a line like this to
`~/.bash_profile`:

```text
export CUSTOM_RUBY_VERSION="2.1.5"
```

## Usage

The base URL is `https://api.codeunion.com/v1/`.

As of now no authentication is required.

## Endpoints

### Search resources

Find resources whose text contains a particular query

```
GET /v1/search?:query_params
```

#### Parameters

Name | Type | Description | Required
-----|------|-------------|---------
query | string | Search query | true
category | string | See supported categories in `app/models/resource.rb` | false

#### Request

```
GET /v1/search?category=examples&query=REST%20API
```

#### Response

```json
[
  {
    "name": "overheard-server",
    "description": "Example project for a web app that stores and shares hilarious, out of context quotess and quips.",
    "private": false,
    "url": "https://github.com/codeunion/overheard-server",
    "category": "examples",
    "tags": [
      "ruby",
      "sinatra",
      "datamapper",
      "sqlite"
    ],
    "access": [
      "public",
      "students",
      "staff"
    ],
    "license": true,
    "has_wiki": false,
    "notes": "",
    "excerpt": "<match>REST</match> <match>API</match> to add and list Overheards\n\nFor a list of planned and implemented features, known bugs, etc. check the\n[CHANGELOG"
  }
]
```
