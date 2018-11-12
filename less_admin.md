# Use without administrator privileges

This extension requires the administrator rights for some actions. However, you can limit the administrator right for 2 actions and delegate the others to an service account for execution.

This table show all actions available in this extension and the right level needed for work:

|-------------------|-----------------|
| Action | Right Needed |
|-------------------|-----------------|
| [win32_continue_service](http://php.net/manual/en/function.win32-continue-service.php) | Service manager right |
| [win32_create_service](http://php.net/manual/en/function.win32-create-service.php) | Administrator right |
| [win32_delete_service](http://php.net/manual/en/function.win32-delete-service.php) | Administrator right |
| [win32_get_last_control_message](http://php.net/manual/en/function.win32-get-last-control-message.php) | Service account set in service configuration |
| [win32_pause_service](http://php.net/manual/en/function.win32-pause-service.php) | Service manager right |
| [win32_query_service_status](http://php.net/manual/en/function.win32-query-service-status.php) | User right |
| [win32_set_service_status](http://php.net/manual/en/function.win32-set-service-status.php) | Service account set in service configuration |
| [win32_start_service_ctrl_dispatcher](http://php.net/manual/en/function.win32-start-service-ctrl-dispatcher.php) |  |
| [win32_start_service](http://php.net/manual/en/function.win32-start-service.php) | Service manager right |
| [win32_stop_service](http://php.net/manual/en/function.win32-stop-service.php) | Service manager right |
|-------------------|-----------------|

## Process

* Create and add the service
* Set the minimal ACL `RPWPRC` onto the service with `sc set`. Note this command overwite all ACL. Read first the current ACL with `sc show`. See [this Microsoft best practices](https://support.microsoft.com/en-us/help/914392/best-practices-and-guidance-for-writers-of-service-discretionary-access-control-lists)
* Enable the win32service extension build from this branch into your PHP installation.
* Use the account with low level privileges for run the PHP script for control the defined service. All work.
Now attempt control another service without set the ACL. Nothing work.
