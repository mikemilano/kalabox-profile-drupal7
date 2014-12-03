# Kalabox Drupal 7 Profile

### Kalabox dev team notes
This profile is a prototype for testing the use of an independent profile project that includes
local and external plugins. `kalabox-plugin-drush` is local and `kalabox-plugin-drupal7`
is a separate npm project defined as a dependency in `package.json`.

## Usage

1. Create a project directory, and a `public` directory inside of it
where the Drupal codebase will be run from.
```
mkdir -p myproject/public
cd myproject
```

2. Clone the drupal7 profile into a `.kalabox` directory.
```
git clone git@github.com:mikemilano/kalabox-profile-drupal7.git .kalabox
```

3. Update `title` and `name` in the `.kalabox/profile.json` file.
```
{
  "title": "My Site Title",
  "name": "my-site",
  ...
```
*Note: `name` must include lowercase alphanumeric characters and hyphens only.*

*Note: This name must be unique to any other kalabox apps on your system.*

4. Initialize your app
```
kbox init
kbox start
```


## Plugin commands provided
```
# download drupal
kbox d7.download

# install drupal (user: admin, password: kalabox)
kbox d7.install

# use drush
kbox drush status
```


## Profile architecture detail

Your project will be mounted into each container at `/src`.

The nginx site config root is set to serve this drupal
instance from `myproject/public` based on the instructions above.

Services used in this profile have been setup to read their
config files from `/src/.kalabox/config`.

For example, within the context of the PHP container,
`/etc/php5/fpm/php.ini` is symlinked from `/src/.kalabox/config/php/php.ini`.

This allows you to modify the files right from your source code.

For services requiring a restart after modifying configurations, simply
restart your kalabox app. `kbox stop && kbox start`.

Dockerfiles defined in this profile are included in core, so they
do not need to exist in this file system.
