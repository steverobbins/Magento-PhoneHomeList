Mirasvit_MstCore
===

:x: Unacceptable

* Event and controller dispatch based phone homes
* Disclosure of possibly sensative information

Affected versions:

* 2.0.0

---

# Admin notifications

In `app/code/local/Mirasvit/MstCore/etc/config.xml`, an event is fired before a controller is dispatched in the admin.

The event name is `controller_action_predispatch` which calls `mstcore/feed_updates::check()`.

In `check()`, if 12 hours have passed from the last time `check()` was called, a feed is requested from `http://mirasvit.com/blog/category/updates/feed/` and items are sent to the admin notification box.

---

# License check

In `app/code/local/Mirasvit/MstCore/etc/config.xml`, an event is fired each time a block is rendered in the admin.

The event name is `core_block_abstract_to_html_after` which calls `Mirasvit_MstCore_Helper_Code::onCoreBlockAbtractToHtmlAfter()`.

The `Mirasvit_MstCore_Helper_Code` class is obfuscated, but when analyzed, reveals that information about the Magento install is being sent (under certain conditions) to `http://mirasvit.com/lc/check/` for a license check.  A request is sent for each `Mirasvit_*` module installed ()excluding `MstCore`).

Information sent includes:

* The current URL
* The server's IP address
* The Magento version
* The Magento edition
* A module identifier
* An md5'd string of the database name and host

If a licensing error is detected, a message received from the check is displayed in place of the block's HTML.
