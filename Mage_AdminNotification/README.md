Magestore_Magenotification
===

:x: Unacceptable

* Controller dispatch based phone homes

Affected versions:

* 0.1.4

---

# Admin notifications

In `app/code/core/Mage/AdminNotification/etc/config.xml`, an event is fired before a controller is dispatched in the admin.

```
<controller_action_predispatch>
    <observers>
        <adminnotification>
            <class>adminnotification/observer</class>
            <method>preDispatch</method>
        </adminnotification>
    </observers>
</controller_action_predispatch>
```

This check will occur if it's been more that 1 - 24 hours (configurable option) since it was last run.

When run, a curl request is sent (with a 2 second timeout) to `http://notifications.magentocommerce.com/community/notifications.rss`.
