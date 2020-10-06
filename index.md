---
title: Win32Service
menus: home
---

# Win32Service project

This project provides most elements:
* a PHP extension for running a custom PHP script like a Windows Service
* a PHP library for help to use the extension
* a Bundle to integrating the library into your Symfony 4 project

## News

For the latest news for this project, search on Twitter the [#Win32Service hashtag](https://twitter.com/hashtag/Win32Service) [![#Win32Service hashtag](https://img.shields.io/twitter/url/https/github.com/win32service/win32service.svg?style=social)](https://twitter.com/hashtag/Win32Service).

## PHP Extension

[![Repository](https://img.shields.io/badge/GitHub-win32service%2Fwin32service-blue.svg)](https://github.com/win32service/win32service)
[![Build status](https://ci.appveyor.com/api/projects/status/7wqljie1knsrtfkh/branch/v0.4.x?svg=true)](https://ci.appveyor.com/project/macintoshplus/win32service/branch/v0.4.x)
[![License](https://img.shields.io/badge/license-PHP_License-blue.svg)](http://www.php.net/license/3_01.txt)
[![Documentation](https://img.shields.io/badge/manual-win32service-blue.svg)](http://php.net/manual/en/book.win32service.php)

## PHP Library

[![Repository](https://img.shields.io/badge/GitHub-win32service%2Fservice--library-blue.svg)](https://github.com/win32service/service-library)
[![Build status](https://ci.appveyor.com/api/projects/status/nm8kqrbokv49mckk?svg=true)](https://ci.appveyor.com/project/macintoshplus/win32servicelib)
[![License](https://img.shields.io/packagist/l/win32service/service-library.svg)](https://github.com/win32service/service-library/blob/master/LICENSE)
[![Documentation](https://img.shields.io/badge/manual-service_library-blue.svg)](https://win32service.github.io/service_library.html)

## Symfony Bundle

[![Repository](https://img.shields.io/badge/GitHub-win32service%2FWin32ServiceBundle-blue.svg)](https://github.com/win32service/Win32ServiceBundle)
[![License](https://img.shields.io/packagist/l/win32service/service-library.svg)](https://github.com/win32service/Win32ServiceBundle/blob/master/LICENSE)
[![Documentation](https://img.shields.io/badge/manual-bundle-blue.svg)](https://win32service.github.io/bundle.html)

## Requirements

### For the extension

* Windows 7 or newer, Windows 2012 R2 or newer
* PHP 7.1 or newer for Windows

### For the library

* You can install this library on all operating system
* PHP 7.1 or newer

### For the Symfony bundle

* You can install this Bundle on all operating system
* Symfony 4 or newer

## Goal

This extension provide a wrapper between Windows Service Manager and your PHP script. The PHP version supported by this extension is 7.1.1 and later.
This extension work only for the Windows Build of PHP and with all variant (NTS/TS and 32/64 bit).

This extension requires the elevated privileges for work. However, you can [delegate for some actions](less_admin.md)

## Download

You can download the pre-build extension from:

* The [official extension website for PHP](http://pecl.php.net/package/win32service) This site provide the slow release.
* The [Github repository tag assets](https://github.com/win32service/win32service/releases) The tags contains the pre-release build.
* The [Appveyor artifact](https://ci.appveyor.com/project/macintoshplus/win32service) The artifact are available since 6 month. The build for all change are available for test only.


## Installation

Unzip the package and copy the extention into the folder `ext` of your PHP installation.

After copy, edit the the file `php.ini` and add one line for load the extension depending on your version of PHP (7.1/7.2/7.3, x64/x86, ZTS/NTS). In example for PHP 7.3 in TS mode and 32 bit architecture : `extension = php_win32service-7.3-ts-vc14-x86.dll` (or use the short name available since PHP 7.2 : `extension = win32service` if the extension file is named `php_win32service.dll`).

Check in command line if the extension is correctly loaded with this command `php --ri win32service`.

If the output indicate this extension is not loaded, check the PHP configuration.

__Note: The PHP version 7.1.0 dont work with this extension, use the latest version of PHP 7.1.__

## Use

You can use this [PHP service-library](https://github.com/win32service/service-library) for implements your service runtime and management scripts.
If you project is based on Symfony 4+, you can use [the bundle](https://github.com/win32service/Win32ServiceBundle) to integrate the library into Symfony and reduce the number of codes do you need to write.

Otherwise , the downloaded zip contains examples scripts used for testing. The file `service.php` contains a skeleton for implement one service in PHP.

To use this example, open a command line window in administrator mode. Go to the example folder and run this command `php service.php create` to installing the test service.

Now a new service is added into the Windows service manager. You can start, stop this service from the Windows service manager or from the administrator command line.

Good coding !

## Help

Crash, feature request, or suggest, please [open an issue](https://github.com/win32service/win32service/issues).

Help for the extension function, visit the [official PHP web site](http://php.net/manual/en/book.win32service.php)

Blog post: [Extension PHP pour réaliser des services Windows [FR]](https://nahan.fr/extension-php-pour-realiser-des-services-windows/)

Blog post: [Nouveautés de Win32Service 0.4 [FR]](https://nahan.fr/nouveautes-de-win32service-0-4/)

Blog posts: [[Win32Service] PHP 7.0 and 7.1 support [EN]](https://nahan.fr/win32service-php-7-0-and-7-1-support/) and [[Win32Service] Support de PHP 7.0 et PHP 7.1 [FR]](https://nahan.fr/win32service-support-de-php-7-0-et-php-7-1/)

## Contributing

If you want to contribute, you can [open an issue](https://github.com/win32service/win32service/issues) for propose your idea. If you can writing the code, [fork the repository](https://github.com/win32service/win32service) and write the code, finally propose your enhancement by a pull request.


<!-- Matomo -->
<script type="text/javascript">
  var _paq = window._paq = window._paq || [];
  /* tracker methods like "setCustomDimension" should be called before "trackPageView" */
  _paq.push(["setDocumentTitle", document.domain + "/" + document.title]);
  _paq.push(["setDoNotTrack", true]);
  _paq.push(['trackPageView']);
  _paq.push(['enableLinkTracking']);
  (function() {
    var u="https://analytics.nahan.fr/";
    _paq.push(['setTrackerUrl', u+'matomo.php']);
    _paq.push(['setSiteId', '3']);
    var d=document, g=d.createElement('script'), s=d.getElementsByTagName('script')[0];
    g.type='text/javascript'; g.async=true; g.src=u+'matomo.js'; s.parentNode.insertBefore(g,s);
  })();
</script>
<noscript><p><img src="https://analytics.nahan.fr/matomo.php?idsite=3&amp;rec=1" style="border:0;" alt="" /></p></noscript>
<!-- End Matomo Code -->