---
title: Service Library
menus: library
permalink: /service-library
---

[return to home](index.md)

The Service library for PHP
---------------------------

This library is [available here](https://github.com/win32service/service-library) for help you to use the [win32service](https://pecl.php.net/package/win32service) extension for PHP.

## Install

This library requires the [Win32Service](https://pecl.php.net/package/win32service) extension for PHP.

```cmd
c:\> composer require win32service/service-library
```

## Use for register or unregister the service

See the example ['example/adminAction.php'](https://github.com/win32service/service-library/blob/master/examples/adminActions.php). The code in this example needs the administrator right.

> Security : Do not execute this from the web request for security reasons.

## Use to manage any services

See the example ['example/managementActions.php'](https://github.com/win32service/service-library/blob/master/examples/managementActions.php). The code in this example needs the administrator rights or a specific account with limited rights.

### With Administrator right

If you execute their actions with the administrator right, please limit the action to the local host. 

> Security : Do not execute this from the web request for security reasons.


### With a service account with limited rights

The recommended way for use remotely their actions is to make a new service account in your ActiveDirectory without any right.

Open the right of the account for each service needed to manage. To open the right, see the [Microsoft Documentation](https://support.microsoft.com/en-us/help/914392/best-practices-and-guidance-for-writers-of-service-discretionary-access-control-lists)

After the service is registered run this command to read the right set on the service 

```cmd
C:\> sc sdshow my_test_service
```

Replace the `my_test_service` by your service identifier to read the information.

> Note : Run this command in cmd administrator console.

The result example:

```
D:(A;;CCLCSWRPWPDTLOCRRC;;;SY)(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;BA)(A;;CCLCSWLOCRRC;;;IU)(A;;CCLCSWLOCRRC;;;SU)S:(AU;FA;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;WD)
```

Get the SID for the service account, with this command:
```cmd
C:\> wmic useraccount where (name='<username>' and domain='<domain_short_name>') get name,sid
```

The response:

```
Name        SID
<username>  S-1-5-21-1553544295-1745644848-8500016-126000
```

Add the string into the right after changing the <SID>:

```
(A;;RPWPRCDT;;;<SID>)
```

The resulst will be gone:

```
(A;;RPWPRCDT;;;S-1-5-21-1553544295-1745644848-8500016-126000)
```

> Note : the `CCLCRPWPRCDT` represent the right to set for the SID. See the [Microsoft Documentation](https://support.microsoft.com/en-us/help/914392/best-practices-and-guidance-for-writers-of-service-discretionary-access-control-lists) to know the representation.

The final right is like this:

```
D:(A;;CCLCSWRPWPDTLOCRRC;;;SY)(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;BA)(A;;CCLCSWLOCRRC;;;IU)(A;;CCLCSWLOCRRC;;;SU)(A;;RPWPRCDT;;;S-1-5-21-1553544295-1745644848-8500016-126000)S:(AU;FA;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;WD)
```

Now, set the new right for the service with the Administrator CMD window:

```cmd
C:\> sc sdset my_test_service D:(A;;CCLCSWRPWPDTLOCRRC;;;SY)(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;BA)(A;;CCLCSWLOCRRC;;;IU)(A;;CCLCSWLOCRRC;;;SU)(A;;RPWPRCDT;;;S-1-5-21-1553544295-1745644848-8500016-126000)S:(AU;FA;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;WD)
```

Replace the `my_test_service` by your service identifier to write the security descriptor.

## Running a service

See the example ['example/service.php'](https://github.com/win32service/service-library/blob/master/examples/service.php).

For running a script as a service, you must be extending the `Win32Service\Model\AbstractServiceRunner` class.
The `run` function is called into the loop and do return before 30s.
If the `run` execution duration is over 30s, the service is marked stopped by the Windows Service Manager.
In this case, the method `lastRunIsTooSlow` is called and the first argument contains the last `run` execution duration.

### Automatic restart the service

Since the version 0.4.0 of the Win32Service extension, you can define the exite mode and exit code.
If the exit mode is not gracefully and the exit code is geater than 0, the recovery setting of the Windows service manager can be used.

In this case, define the action for first, second and next fail of the service to `restart` value.


### Usage with Symfony

For use with Symfony, define an `Command` and inject into your service class. Add an InputOption named `max-run` for define
the number of loop executed between each service restart.

In the `execute` function call the service `doRun` function with the max-run value.


## Run tests

> Prerequisites : [Composer](https://getcomposer.org) is installed on your computer.

After clone or download the [repository](https://github.com/win32service/service-library) open CMD window and go to the project directory.
Run this command for download needed dependencies:

```cmd
c:\> composer install -o
```

And run Atoum for tests:

```cmd
c:\> vendor/bin/atoum.bat
```

## Help

Crash, feature request, or suggest, please [open an issue](https://github.com/win32service/service-library/issues).

## Contributing

If you want to contribute, you can [open an issue](https://github.com/win32service/service-library/issues) to propose your idea.
If you can write the code, fork the [repository](https://github.com/win32service/service-library) and write the code, finally submit your enhancement by a pull request.

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
