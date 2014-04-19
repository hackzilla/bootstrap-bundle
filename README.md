Boostrap Helper Bundle for Symfony2
===================================

Requirements
------------

* java
* nodejs
* cssembed [http://www.java2s.com/Code/Jar/c/cssembed.htm]
* yuicompressor [https://github.com/yui/yuicompressor/downloads]

Installation
------------

Copy cssembed.jar, and yuicompressor.jar to /app/Resources/java/

Add to config.yml

```yml
# Twig Configuration
twig:
    form:
        resources:
          - 'HackzillaBoostrapkBundle:Form:fields.html.twig'
```

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

(Re)Generate bootstrap.js and bootstrap.css
-------------------------------------------

```
app/console assetic:dump --env=prod --no-debug;
app/console assetic:dump --env=dev;
```

Advanced usage
==============

Copy @HackzillaBootstrapBundle/Resources/less/compile.less and @HackzillaBootstrapBundle/Resources/less/variables.less to your own folder resources folder, and update your config.


