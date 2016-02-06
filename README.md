## Openshift Nginx/OpenResty Cartridge

A cartridge for openshift that enables Nginx/LuaJIT to be used as the web server.

### Installation

To install this cartridge:

    rhc create-app myapp https://raw.githubusercontent.com/katlogic/openshift-openresty-cartridge/master/metadata/manifest.yml

### Configuration

The cartridge installs two main config files. One at `$OPENSHIFT_NGINX_DIR/conf/nginx.conf`
which gets loaded by the executable and sets up specific app configuration such as logs and
pid files. Its template `$OPENSHIFT_NGINX_DIR/conf/nginx.conf.erb` is meant to be modified
only in the cartridge repo.

The above config then includes another nginx.conf which must exist at `$OPENSHIFT_REPO_DIR/nginx.conf`.
This config should contain all your server specific set up including which ip/port to listen on.

The second nginx.conf is actually seen in your repository as `nginx.conf.erb` so environment
variables can be used in the config. Every time the server starts it first processes `nginx.conf.erb`.

Finally, there is `$OPENSHIFT_REPO_DIR/apps/\*/\*.conf.erb` directory structure, where you can deploy
individual lua apps through your gear repository (hence the additional directory layer).

A `public/` folder is included where static content is served by default. However, as can be seen
in the `nginx.conf.erb` file it is entirely configurable and only exists as a form of documentation.
