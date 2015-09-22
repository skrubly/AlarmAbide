# AlarmAbide

## Example use in batch script##

# First check, notice resource1 and resource2 show critical
$ bash fake_alert_check.sh
First Check to see if we should alert for all
Continues to second check
Critical for resource: resource1
Critical for resource: resource2

# Disable for all resources
$ python alarmabide.py create /tmp/monitors/ test_alert all 60

# Doesn't go past first check
$ bash fake_alert_check.sh
First Check to see if we should alert for all
OK for alert test_alert

# waited 60 seconds and ran again. Now it continues and alerts for each
$ bash fake_alert_check.sh
First Check to see if we should alert for all
Continues to second check
Critical for resource: resource1
Critical for resource: resource2

# Let's not alert for resource1
$ python alarmabide/alarmabide.py create /tmp/monitors/ test_alert resource1 20

# Verified, resource1 is OK
$ bash fake_alert_check.sh
First Check to see if we should alert for all
Continues to second check
OK for resource: resource1
Critical for resource: resource2

# Let's not alert for resource2 as well as resource1
$ python alarmabide/alarmabide.py create /tmp/monitors/ test_alert resource2 20

# Verified both resource1 and resource2 are OK
$ bash fake_alert_check.sh
First Check to see if we should alert for all
Continues to second check
OK for resource: resource1
OK for resource: resource2

# Waited the 20 seconds and ran again. Both alerting again!
$ bash fake_alert_check.sh
First Check to see if we should alert for all
Continues to second check
Critical for resource: resource1
Critical for resource: resource2
