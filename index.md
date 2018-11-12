# Win32Service projet

This projet provide an PHP extension for running a custom PHP script like a Windows Service.

## Goal

This extension provide a wrapper between Windows Service Manager and your PHP script. The PHP version supported by this extension is 7.0.1 and later.
This extension work only for the Windows Build of PHP and with all variant (NTS/TS and 32/64 bit).

This extension requires the elevated privileges for work. However, you can [delegate for some actions](less_admin.md)

## Download

You can download the pre-build extension from:

* The [official extension website for PHP](http://pecl.php.net/package/win32service) This site provide the slow release.
* The [Github repository tag assets](https://github.com/win32service/win32service/releases) The tags contains the pre-release build.
* The [Appveyor artifact](https://ci.appveyor.com/project/macintoshplus/win32service) The artifact are available since 6 month. The build for all change are available for test only.

## Installation

Unzip the package and copy the extention into the folder `ext` of your PHP installation.

After copy, edit the the file `php.ini` and add one line for load the extension depending on your version of PHP (7.0/7.1/7.2/7.3, x64/x86, ZTS/NTS). In example for PHP 7.3 in TS mode and 32 bit architecture : `extension = php_win32service-7.3-ts-vc14-x86.dll` (or use the short name available since PHP 7.2 : `extension = win32service` if the extension file is named `php_win32service.dll`).

Check in command line if the extension is correctly loaded with this command `php --ri win32service`.

If the output indicate this extension is not loaded, check the PHP configuration.

## Use

The downloaded zip contain examples scripts used for testing. The file `service.php` contains an skeleton for implement one service in PHP.

For use this example, open an command line window in administrator mode. Go to the example folder and run this command `php service.php create` for install the test service.

Now a new service is added into the Windows service manager. You can start, stop this service from the Windows service manager or from the administrator command line.

Good coding !

## Help

Crash, feature request, or suggest, please open an issue.

Help for the extension function, visit the [official PHP web site](http://php.net/manual/en/book.win32service.php)

[Extension PHP pour réaliser des services Windows [FR]](https://nahan.fr/extension-php-pour-realiser-des-services-windows/)

## Contributing

If you want contribute, you can open an issue for propose your idea. If you can writing the code, fork this repository and write the code, finally propose your enhancement by a pull request.

