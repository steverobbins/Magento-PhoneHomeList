Magestore_Magenotification
===

:x: Unacceptable

* Controller dispatch based phone homes

Affected versions:

* 0.1.4

---

# Admin notifications

In `app/code/local/Magestore/Magenotification/etc/config.xml`, an event is fired before a controller is dispatched in the admin.

```
<controller_action_predispatch>
    <observers>
      <magestore_magenotification_observer>
        <type>singleton</type>
        <class>magenotification/observer</class>
        <method>controllerActionPredispatch</method>
      </magestore_magenotification_observer>
   </observers> 
</controller_action_predispatch>
```

This check will occur if it's been more that 24 hours since it was last run.

When run, a curl request is sent (with a 2 second timeout) to `http://www.magestore.com/index.php/magenotification/service/getfeed3/lastupdatetime/<DATE>`.
