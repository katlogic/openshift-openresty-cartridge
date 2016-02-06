## Openshift Nginx/OpenResty Cartridge

A cartridge for openshift that enables Nginx/LuaJIT to be used as the web server.

### Installation

To install this cartridge:

	rhc create-app myapp https://raw.githubusercontent.com/katlogic/openshift-openresty-cartridge/master/metadata/manifest.yml

### Configuration

The cartridge installs two main config files. One at <code>$OPENSHIFT_NGINX_DIR/conf/nginx.conf</code> which gets loaded by the executable and sets up specific app configuration such as logs and pid files. Its template <code>$OPENSHIFT_NGINX_DIR/conf/nginx.conf.erb</code> is meant to be modified only in the cartridge repo.

The above config then includes another nginx.conf which must exist at <code>$OPENSHIFT_REPO_DIR/nginx.conf</code>. This config should contain all your server specific set up including which ip/port to listen on.

The repo nginx.conf is actually seen in your repository as <code>nginx.conf.erb</code> so environment variables can be used
in the config. Every time the server starts it first processes <code>nginx.conf.erb</code>.

Finally, there is <code>$OPENSHIFT_REPO_DIR/apps/*/*.conf.erb</code> structure, where you can deploy individual lua apps through your repository (hence the additional directory layer).

A <code>public/</code> folder is included where static content is served by default. However, as can be seen in the <code>nginx.conf.erb</code> file it is entirely configurable and only exists as a form of documentation.
