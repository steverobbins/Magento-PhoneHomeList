Aitoc_Aitsys
===

:x: Unacceptable

* Controller dispatch based phone homes

Affected versions:

* 3.2.1

---

# Admin notifications

In `app/code/community/Aitoc/Aitsys/etc/config.xml`, an event is fired before a controller is dispatched in the admin.

```
<controller_action_predispatch>
    <observers>
        <ambase_upds>
            <type>singleton</type>
            <class>aitsys/observer</class>
            <method>updateNotification</method>
        </ambase_upds>
    </observers>
</controller_action_predispatch>
```

This check will occur if it's been more that 24 hours since it was last run.

When run, a curl request is sent (with a 2 second timeout) to `http://www.aitoc.com/en/feedrss`.
