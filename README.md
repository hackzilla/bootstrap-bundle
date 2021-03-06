Boostrap Helper Bundle for Symfony2
===================================

Requirements
------------

* java
* nodejs (npm & less)
* cssembed [https://github.com/nzakas/cssembed/downloads]
* yuicompressor [https://github.com/yui/yuicompressor/downloads]

System Setup
------------

For ubuntu, run the following commands to install necessary dependencies.

```bash
apt-get install java-common nodejs npm
npm install -g less
```

Installation
------------

Add HackzillaBootstrapBundle in your composer.json:

```json
{
    "require": {
        "hackzilla/bootstrap-bundle": "~0.2",
    }
}
```

Now tell composer to download the bundle by running the command:

``` bash
$ php composer.phar update hackzilla/bootstrap-bundle
```

Composer will install the bundle into your project's `vendor/hackzilla` directory.

### Step 2: Enable the bundle

Enable the bundle in the kernel:

``` php
<?php
// app/AppKernel.php

public function registerBundles()
{
    $bundles = array(
        // ...
        new Hackzilla\Bundle\BootstrapBundle\HackzillaBootstrapBundle(),
        // ...
        // Your application bundles
    );
}
```

Copy cssembed.jar, and yuicompressor.jar to /app/Resources/java/

Add to config.yml

```yml
# Twig Configuration
twig:
    form:
        resources:
          - 'HackzillaBoostrapBundle:Form:fields.html.twig'
```

If nodejs path is different on your system, then update it here.

Possible values are:
* /usr/local/bin/node
* /usr/bin/node
* /usr/bin/nodejs

```yml
# Assetic Configuration
assetic:
    java: /usr/bin/java
    filters:
      cssembed:
        jar: %kernel.root_dir%/Resources/java/cssembed-<version>.jar
      cssrewrite: ~
      yui_js:
        jar: %kernel.root_dir%/Resources/java/yuicompressor-<version>.jar
      less:
          node: /usr/local/bin/node
          node_paths: [/usr/local/lib/node_modules]
          apply_to: "\.less$"
    assets:
      bootstrap_js:
          inputs:
              - '%kernel.root_dir%/../vendor/twbs/bootstrap/js/affix.js'
              - '%kernel.root_dir%/../vendor/twbs/bootstrap/js/alert.js'
              - '%kernel.root_dir%/../vendor/twbs/bootstrap/js/button.js'
              - '%kernel.root_dir%/../vendor/twbs/bootstrap/js/carousel.js'
              - '%kernel.root_dir%/../vendor/twbs/bootstrap/js/collapse.js'
              - '%kernel.root_dir%/../vendor/twbs/bootstrap/js/dropdown.js'
              - '%kernel.root_dir%/../vendor/twbs/bootstrap/js/modal.js'
              - '%kernel.root_dir%/../vendor/twbs/bootstrap/js/tooltip.js'
              - '%kernel.root_dir%/../vendor/twbs/bootstrap/js/popover.js'
              - '%kernel.root_dir%/../vendor/twbs/bootstrap/js/scrollspy.js'
              - '%kernel.root_dir%/../vendor/twbs/bootstrap/js/tab.js'
              - '%kernel.root_dir%/../vendor/twbs/bootstrap/js/transition.js'
          filters: [?yui_js]
      bootstrap_less:
          inputs:
              - '@HackzillaBootstrapBundle/Resources/less/compile.less'
          filters: [less,cssembed]
```

- [Example base.html.twig](Resources/doc/base.html.twig)


Fonts
-----

in web directory create symlink to the bootstrap fonts

```ln -s  ../vendor/twbs/bootstrap/fonts```


(Re)Generate bootstrap.js and bootstrap.css
-------------------------------------------

```
app/console assetic:dump --env=prod --no-debug;
app/console assetic:dump --env=dev;
```

Advanced usage
==============

Copy @HackzillaBootstrapBundle/Resources/less/compile.less and @HackzillaBootstrapBundle/Resources/less/variables.less to your own folder resources folder, and update bootstrap_less section in your config.

~~Alternatively copy @HackzillaBootstrapBundle/Resources/less/variables.less to /app/Resources/HackzillaBootstrapBundle/less/variables.less~~
