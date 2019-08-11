# Shellinabox S3 (Sass Style System)

#### About shellinabox

> Shell In A Box implements a web server that can export arbitrary command line tools to a web based terminal emulator. This emulator is accessible to any JavaScript and CSS enabled web browser and does not require any additional browser plugins.


## Description

Shellinabox S3 (Sass Style System) aims to provide a layer of customization over Shellinabox. This is an adaptation for [apnscp](https://apnscp.com) based off the work by [Matteo Drera](https://github.com/sevenissimo/shellinabox-s3).

Unlike default _monolithic built-in stylesheet_, this project breaks down terminal emulator CSS into _smaller, customizable, modular_ parts. To do that it makes the most of [SASS language](http://sass-lang.com/).


## Quick start

Some stylesheets from this project are bundled with apnscp 3.1. Use of this project requires apnscp 3.1+. Use `cpcmd misc:cp-version` to get your current panel version.


## Build

1. Clone repository
    ```bash
    cd /usr/local/apnscp/build
    git clone https://github.com/apisnetworks/shellinabox-themes.git
    cd shellinabox-themes
    ```
    
2. Install sassc + dependencies 
   ```bash
   yum install -y sassc
   ```

3. Edit SASS and Makefile to suit needs. Build CSS by running `make` in project directory.
  - This will generate `build/shellinabox.css` and some `build/theme-*.css`.
  - A list of themes to be built may always be specified with:  
  ```bash
  make THEMES="solarized-light solarized-dark"
  ```
  ​	where `THEMES` value must be a **space separated list** or special keyword `ALL`.  
  
- There must be valid corresponding SCSS files into `sass/themes/` in order to work correctly.  
  
4. Install. Run `make install`, then restart shellinaboxd with `make restart`. Voila! Themes are copied into `config/custom/apps/terminal/shellinabox/share/css`.

#### Setting default theme
Use the apnscp.config scope:
```bash
cpcmd config:set apnscp.config ssh theme "greenscreen dark"
make restart
```
Theme name must be in lowercase

### Monolithic build
It is possible to build a monolithic `shellinabox.css` with a single theme built-into.
To do that:

+	edit `config.scss` and set option `$enable-external-themes: false;`.
+	edit `shellinabox.scss` to import a theme: `@import "themes/theme.scss";`

Then set the default theme for SSH to "",
```bash
cpcmd config:set apnscp.config ssh theme ""
make restart
```
*Setting `ssh theme null` would reset to the default theme provided in config/config.ini!*

## Customization
Customization, other than theme switching, can be accomplished by direct modify Sass variables, maps, and custom CSS.

Here's a list of relevant files:

- `themes/*.scss`: define themes own properties like colors schemes.

	You could create your own theme, place it here, and run `make THEMES="my-theme"`

- `config.scss`: main configuration file for colors, options, fonts, etc.

	Every SASS variable defined here includes the `!default` flag, so a theme can override these.
	You could edit these values, anyhow, avoid importing a theme here to grant external themes to be generated correctly.

- `shellinabox.scss` main stylesheet file.

	No need to import a theme here unless you disabled external themes (see [monolithic build](#monolithic-build)).


#### More information:

* [Manual page](https://github.com/shellinabox/shellinabox/wiki/shellinaboxd_man)
* [Github mirror](https://github.com/shellinabox/shellinabox/)
* [Official site](https://code.google.com/p/shellinabox)
* [Official wiki](https://code.google.com/p/shellinabox/wiki/shellinaboxd_man)