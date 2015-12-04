Amasty_Base
===

:neutral_face: Tolerable

* Controller dispatched phone homes but can be disabled via admin config

Affected versions:

* 2.1.3

---

# Admin notifications

In `app/code/local/Amasty/Base/etc/config.xml` *and* `app/code/local/Amasty/Base/etc/adminhtml.xml`, an event is fired before a controller is dispatched in the admin.

```
<events>
    <controller_action_predispatch>
        <observers>
            <ambase_upds>
                <type>singleton</type>
                <class>ambase/feed</class>
                <method>check</method>
            </ambase_upds>
        </observers>
    </controller_action_predispatch>
</events>
```

This check will occur if it's been more that 24 hours since it was last run.

When run, a curl request is sent (with a 2 second timeout) to `http://amasty.com/feed-extensions.xml`.

It is possible to disable this by updating your config in **Amasty Extensions** > **Extensions & Notifications** > **Notifications**.

![Feed Settings](https://i.imgur.com/KeRfsdc.png)

