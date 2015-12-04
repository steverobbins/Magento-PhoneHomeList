Itoris_Installer
===

:x: Unacceptable

Affected versions:

* 2.1.7

---

# Admin notifications

In `app/code/local/Itoris/Installer/etc/config.xml`, an event is fired before a controller is dispatched in the admin.

```
<events>
    <controller_action_predispatch>
        <observers>
            <itoris_installer_notifications>
                <class>itoris_installer/notifications</class>
                <method>checkUpdates</method>
            </itoris_installer_notifications>
        </observers>
    </controller_action_predispatch>
</events>
```

It appears this check will occur if it's been more that 24 hours since it was last run.  However, the `Itoris_Installer_Model_Notifications` is heavily obfuscated and it hasn't been confirmed that the configuration value is being honored.

This module cannot be disabled without breaking other `Itoris_*` modules.  However, replacing the contents of `app/code/local/Itoris/Installer/` with [these contents](replacement) has proven to be effective.
