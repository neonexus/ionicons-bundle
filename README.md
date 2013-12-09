CodingfogeyFontAwesomeBundle
============================

[![SensioLabsInsight](https://insight.sensiolabs.com/projects/7b8a98ea-e8e8-49c0-a5b0-7ee378009b07/mini.png)](https://insight.sensiolabs.com/projects/7b8a98ea-e8e8-49c0-a5b0-7ee378009b07)
[![Total Downloads](https://poser.pugx.org/codingfogey/fontawesome-bundle/downloads.png)](https://packagist.org/packages/codingfogey/fontawesome-bundle)
[![Latest Stable Version](https://poser.pugx.org/codingfogey/fontawesome-bundle/v/stable.png)](https://packagist.org/packages/codingfogey/fontawesome-bundle)
[![Latest Unstable Version](https://poser.pugx.org/codingfogey/fontawesome-bundle/v/unstable.png)](https://packagist.org/packages/codingfogey/fontawesome-bundle)
[![Build Status](https://travis-ci.org/codingfogey/fontawesome-bundle.png)](https://travis-ci.org/codingfogey/fontawesome-bundle)
[![Scrutinizer Quality Score](https://scrutinizer-ci.com/g/codingfogey/fontawesome-bundle/badges/quality-score.png?s=ddf3507ab8055474b46db51a92e7a486a94a931a)](https://scrutinizer-ci.com/g/codingfogey/fontawesome-bundle/)
[![Code Coverage](https://scrutinizer-ci.com/g/codingfogey/fontawesome-bundle/badges/coverage.png?s=b9f564491938c725b1dc2f64b1461071a6b710cf)](https://scrutinizer-ci.com/g/codingfogey/fontawesome-bundle/)

[![knpbundles.com](http://knpbundles.com/codingfogey/fontawesome-bundle/badge-short)](http://knpbundles.com/codingfogey/fontawesome-bundle)

About
-----

This Bundle makes it easy to integrate [Font Awesome](http://fortawesome.github.io/Font-Awesome/) into your [Symfony2](http://symfony.com/) projects.


Prerequisites
-------------

- Font Awesome installed somewhere in your project. It is not contained in this bundle. You can use [Composer](http://getcomposer.org), [Bower](http://bower.io) or any other way to install it.


Installation
------------

1. Add `codingfogey/fontawesome-bundle` to your `composer.json`:

        {
            ...
            "require": {
                ...
                "codingfogey/fontawesome-bundle": "dev-master",
                "fortawesome/font-awesome": "v4.0.3"
            }
            ...
        }

2. Add `CodingfogeyFontAwesomeBundle` to your `AppKernel.php`:

        ...
        public function registerBundles()
        {
            $bundles = array(
                ...
                new Codingfogey\Bundle\FontAwesomeBundle\CodingfogeyFontAwesomeBundle()
            );
            ...
        }
        ...

3. Update your dependencies: `composer update`.

NOTICE Installing Font Awesome via composer is optional but makes this bundle work out of the box. So I recommend this way.


Configuration
-------------

If you did not install Font Awesome via composer you have to configure the path to your installation:

    codingfogey_font_awesome:
        assets_dir: %kernel.root_dir%/../vendor/fortawesome/font-awesome


Customization
-------------

If you want to customize Font Awesome you have to put a customized variables file somewhere in your project and configure the path. You also have to set the output path.

    codingfogey_font_awesome:
        filter: less
        customize:
            variables_file:         %kernel.root_dir%/Resources/fontawesome/variables.less
            font_awesome_output:    %kernel.root_dir%/Resources/less/fontawesome.less

If you want to use the `lessphp` or `sass` Assetic filter you have to set the `filter` variable accordingly.

There is a command to generate a customized output file to incorporate your customized variables file:

    app/console codingfogey:fontawesome:generate


Usage
-----

The bundle provides a command to install the font files to the `web/fonts` directory:

    app/console codingfogey:fontawesome:install
    
There is also a `ScriptHandler` for conveniently doing this automatically on each `composer install` or `composer update`:

    ...
    "scripts": {
        "post-install-cmd": [
            ...
            "Codingfogey\\Bundle\\FontAwesomeBundle\\Composer\\ScriptHandler::install"
        ],
        "post-update-cmd": [
            ...
            "Codingfogey\\Bundle\\FontAwesomeBundle\\Composer\\ScriptHandler::install"
        ]
    },
    ...

To include the Font Awesome css just include `@fontawesome_css` in your base template.

    <!DOCTYPE html>
    <html>
        <head>
            <meta charset="UTF-8" />
            <title>{% block title %}Welcome!{% endblock %}</title>
            {% block stylesheets %}
                {% stylesheets
                    '@fontawesome_css'
                %}
                    <link rel="stylesheet" href="{{ asset_url }}" media="screen"/>
                {% endstylesheets %}
            {% endblock %}
    
Additionally it provides two [Twig](http://twig.sensiolabs.org/) functions to include icons. 

NOTICE: Currently these functions do not work if you changed the `@fa-css-prefix` variable.

Simple Icons can be added with the `fa_icon( icon [, options] )` function. It takes one or two parameters:

1. the name of the icon which can be looked up [here](http://fortawesome.github.io/Font-Awesome/icons/). Omit the `fa-` prefix.
2. optional JSON with options to customize the icon

This function will create something similar to

    <i class="fa fa-edit fa-border"></i>

The complete optionset looks like follows. By default none of these options are set.

    {
        scale:          [lg|2x|3x|4x|5x|stack-1x|stack-2x],
        fixed-width:    [true|false],
        list-icon:      [true|false],
        border:         [true|false],
        pull:           [left|right],
        spin:           [true|false],
        rotate:         [90|180|270],
        flip:           [horizontal|vertical],
        inverse:        [true|false],
        classes:        <a string of space separeted css classes>
    }


Stacked Icons can be added with the `fa_stacked_icon( icon1, icon2 [, options1 [, options2 [, options]]] )` function. It takes two to five parameters:

1. the name of the foreground icon
2. the name of the background icon
3. options for the foreground icon
4. options for the background icon
2. options for the container element

This function will create something similar to

    <span class="fa-stack">
      <i class="fa fa-circle fa-stack-2x"></i>
      <i class="fa fa-flag fa-stack-1x fa-inverse"></i>
    </span>


TODO
----

Look [here](../../issues?milestone=&state=open).


License
-------

- This bundle is licensed under the [MIT License](http://opensource.org/licenses/MIT).
- For Font Awesome you can find licensing information [here](http://fortawesome.github.io/Font-Awesome/license/).


Acknowledgment
--------------

- This bundle is mainly inspired by [braincrafted/bootstrap-bundle](https://github.com/braincrafted/bootstrap-bundle.git) and most of the code is taken from there.
