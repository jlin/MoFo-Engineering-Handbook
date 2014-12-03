# MoFo Security - Keys and Passwords

## Lastpass
Mozilla Foundation Engineering utilizes [Lastpass](https://lastpass.com) to manage, store, and share the following things in shared folders.
  * Engineer / Application AWS Access Keys/Secret Keys
  * Application-specific SSH private keys
  * SSL Certificate private keys
  * Shared service logins (Heroku, Geckoboard, etc...)

## Getting Started

This section covers how to get Appmaker running locally. The workflow is optimized for contributors.

### Dependencies

Make sure you have `nodejs`, `npm`, and `git` installed.

`grunt` is required to run the test suite. To install grunt on unix and OS X,
run `sudo npm install -g grunt-cli`.

We manage client-side dependencies using [bower](http://bower.io/). In order to add/remove these dependencies, you need to have `bower` installed globally on your machine, which can be done on unix and OS X via
`sudo npm install bower -g`.

[Webmaker Login](https://github.com/mozilla/login.webmaker.org) is required to log into the app. [Follow these instructions exactly](https://github.com/mozilla/login.webmaker.org#getting-the-server-up-and-running-locally) to run it locally

### Forking And Cloning The Repository

Create a root `mozilla-appmaker` directory:
```
mkdir mozilla-appmaker
cd mozilla-appmaker
```

[Fork](https://help.github.com/articles/fork-a-repo) this repository, and
then clone your fork into the `mozilla-appmaker` directory:
```
git clone git@github.com:<your GitHub username>/appmaker.git appmaker
```

Your directory structure should look like this:
```
mozilla-appmaker/
  ├── appmaker/
```

Configure remote:
```
cd appmaker
git remote add upstream git@github.com:mozilla-appmaker/appmaker.git
git fetch upstream
```

### Environment Setup And Configuration

Install Node packages:
```
npm install
```

Configure your env:
```
cp sample.env .env
```

A short explanation of a complete `.env` file:

```
MONGO_URL: REQUIRED - the URI for your mongod instance and database, for example mongodb://localhost/appmakerdev (or whatever your database is named)
COOKIE_SECRET: A long, complex string for cookie encryption (NOTE: You define this for your local use, the string can be anything).
STORE: Storage approach for publishing apps. `local` is the default, `s3` requires additional environment variables (prefixed by S3_)
S3_BUCKET: S3 bucket name. e.g. "my.coolappmaker.com"
S3_KEY: An access key for the S3 bucket listed above.
S3_SECRET: The secret corresponding to the specified S3 access key.
S3_OBJECT_PREFIX: String to prepend S3 objects. Useful for storing objects in folders. E.g. "level1/level2" => <bucket>/level1/level2/<filename>.
PUBLISH_URL_PREFIX: String to prepend to filenames that are saved when publishing. Try use the URL that matches the protocol from which assets are hosted to avoid mixed content blockage.
PERSONA_AUDIENCE: The hostname and port of Appmaker used by Persona for authentication
PORT: The port that the web process listens on for incomming connections
GITHUB_TOKEN: A personal Github token used for loading lists of components from the mozilla-appmaker org during development (https://github.com/blog/1509-personal-api-tokens)
EXCLUDED_COMPONENTS: A comma-delimited list of component repositories to exclude from the mozilla-appmaker org. The name is the repo name rather than the component name, though this is usually the same.
BUNDLE: Any non-null value will cause the application to bundle as many resources as possible
LOAD_FROM_GITHUB: if omitted, or "false", instructs appmaker to load components from repositories hosted on github.com
```

### Install and run MongoDB

1. Install from MongoDB installation packages, brew, apt-get, etc
2. Either configure MongoDB to run on startup or manually start the mongod daemon. You can also run mongod from foreman by adding it to your Procfile
```
mongod
```

### Start the Server

```
foreman start
```

or

```
foreman start -p <PORT>
```

If you need foreman:

```
sudo gem install foreman
```

NOTE: foreman's configuration file is Procfile in the root of the appmaker directory
Foreman explanation: http://blog.daviddollar.org/2011/05/06/introducing-foreman.html

## How you can help

* Fix issues by [submitting Pull Requests](#submitting-a-pull-request)
* Submit new components (See [Component Docs](./doc/en-US))
* Add [issues](https://github.com/mozilla-appmaker/appmaker/issues)
* Build apps
* Run workshops
* Join our weekly call

## Component Development
Required reading:
https://github.com/mozilla-appmaker/appmaker/blob/develop/public/ceci/README.md

Ceci is a set of foundational elements used in a AppMaker app, implemented as a set of [Polymer](http://polymer-project.org/) components.
If you create a new component, it's really an HTML tag that Polymer processes and then injects a variety of capabilities into that tag / JS object

### Example AppMaker Component
TODO link to the Counter example, provide explanation

## Submitting A Pull Request

Switch to develop branch:
```
cd mozilla-appmaker/appmaker
git checkout develop
```

Pull the latest version:
```
git pull
```

Create a new branch (for example a feature branch):
```
git checkout -b your-feature-branch-name
```

Make changes to the local copy, commit your changes, and then make
sure your patch still works with latest version of develop branch:
```
git checkout develop
git pull
git checkout your-feature-branch-name
git rebase develop
```

Test commits:
```
grunt
```

Submit changes:
```
git push origin your-feature-branch-name
```

Submit the pull request at https://github.com/mozilla-appmaker/appmaker. For
more assistance, see Github's help page on [creating a pull request](https://help.github.com/articles/creating-a-pull-request).

## Localization

Appmaker uses the [Webmaker-i18n](https://github.com/mozilla/node-webmaker-i18n) module for localization of both the designer and (ceci) components.

### Localizating component

If you have created your own component, see: https://github.com/mozilla-appmaker/appmaker/wiki/How-components-are-built#localization

### Help on translation

Spotted any typo or want to help translate appmaker into your own language?

Appmaker uses [Transifex](https://transifex.com) for translation platform. You can check this [how to article](https://support.mozilla.org/en-US/kb/translate-webmaker) if you want to contribute for translation and visit [Appmaker on Transifex](https://www.transifex.com/projects/p/mozilla-appmaker) to start translate.