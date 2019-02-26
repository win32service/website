

[return to home](index.md)

# Use without administrator privileges

This extension requires the administrator rights for some actions. However, you can limit the administrator right for 2 actions and delegate the others to an service account for execution.

This table show all actions available in this extension and the right level needed for work:

|-------------------|-----------------|
| Action            | Right Needed    |
|-------------------|-----------------|
| [win32_continue_service](http://php.net/manual/en/function.win32-continue-service.php) | Service manager right |
| [win32_create_service](http://php.net/manual/en/function.win32-create-service.php) | Administrator right |
| [win32_delete_service](http://php.net/manual/en/function.win32-delete-service.php) | Administrator right |
| [win32_get_last_control_message](http://php.net/manual/en/function.win32-get-last-control-message.php) | Service account set in service configuration |
| [win32_pause_service](http://php.net/manual/en/function.win32-pause-service.php) | Service manager right |
| [win32_query_service_status](http://php.net/manual/en/function.win32-query-service-status.php) | User right |
| [win32_send_custom_control](http://php.net/manual/en/function.win32-send-custom-control.php) | User right |
| [win32_start_service_exit_mode](http://php.net/manual/en/function.win32-start-service-exit-mode.php) | Service account set in service configuration |
| [win32_start_service_exit_code](http://php.net/manual/en/function.win32-start-service-exit-code.php) | Service account set in service configuration |
| [win32_set_service_status](http://php.net/manual/en/function.win32-set-service-status.php) | Service account set in service configuration |
| [win32_start_service_ctrl_dispatcher](http://php.net/manual/en/function.win32-start-service-ctrl-dispatcher.php) | Service account set in service configuration |
| [win32_start_service](http://php.net/manual/en/function.win32-start-service.php) | Service manager right |
| [win32_stop_service](http://php.net/manual/en/function.win32-stop-service.php) | Service manager right |
|-------------------|-----------------|

## Process

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
