# zbx2mtrx
A script to send Zabbix notifications to matrix

## Intro
This script is a quick and dirty prove of concept, use at your own risk, it has known bugs

It receives a json message from zabbix and does beautiful things with it.
If the message isn't json, it's just passed to matrix as is.

## Known Bugs
  - using double quotes " in trigger names break the json

## Requirements
  - jq
  - curl

## Hook it up
  - place the script at `/usr/lib/zabbix/alertscripts/matrix` or wherever
  - place the `matrix.conf` at `/usr/lib/zabbix/etc/matrix.conf`
    - fill in AT, HS and ROOMID
  - create a media type in zabbix → administration → media types
    - add those script parameters:
      - {ALERT.SENDTO}
      - {ALERT.SUBJECT}
      - {ALERT.MESSAGE}
    - in `message templates`, add the following templates for problem, recovery and update
      - Discovery and Autoregistration aren't implemented yet, you can take the default ones

### message templates
    {"type":"problem","event":{"time":"{EVENT.TIME}","date":"{EVENT.DATE}","name":"{EVENT.NAME}","nseverity":"{EVENT.NSEVERITY}","severity":"{EVENT.SEVERITY}","opdata":"{EVENT.OPDATA}","id":"{EVENT.ID}","recovery":{"time":"{EVENT.RECOVERY.TIME}","date":"{EVENT.RECOVERY.DATE}"},"update":{"action":"{EVENT.UPDATE.ACTION}","date":"{EVENT.UPDATE.DATE}","time":"{EVENT.UPDATE.TIME}","message":"{EVENT.UPDATE.MESSAGE}"},"duration":"{EVENT.DURATION}","status":"{EVENT.STATUS}","age":"{EVENT.AGE}","ack":{"status":"{EVENT.ACK.STATUS}"}},"host":{"name":"{HOST.NAME}"},"trigger":{"url":"{TRIGGER.URL}"},"user":{"fullname":"{USER.FULLNAME}"}}

    {"type":"recovery","event":{"time":"{EVENT.TIME}","date":"{EVENT.DATE}","name":"{EVENT.NAME}","nseverity":"{EVENT.NSEVERITY}","severity":"{EVENT.SEVERITY}","opdata":"{EVENT.OPDATA}","id":"{EVENT.ID}","recovery":{"time":"{EVENT.RECOVERY.TIME}","date":"{EVENT.RECOVERY.DATE}"},"update":{"action":"{EVENT.UPDATE.ACTION}","date":"{EVENT.UPDATE.DATE}","time":"{EVENT.UPDATE.TIME}","message":"{EVENT.UPDATE.MESSAGE}"},"duration":"{EVENT.DURATION}","status":"{EVENT.STATUS}","age":"{EVENT.AGE}","ack":{"status":"{EVENT.ACK.STATUS}"}},"host":{"name":"{HOST.NAME}"},"trigger":{"url":"{TRIGGER.URL}"},"user":{"fullname":"{USER.FULLNAME}"}}

    {"type":"update","event":{"time":"{EVENT.TIME}","date":"{EVENT.DATE}","name":"{EVENT.NAME}","nseverity":"{EVENT.NSEVERITY}","severity":"{EVENT.SEVERITY}","opdata":"{EVENT.OPDATA}","id":"{EVENT.ID}","recovery":{"time":"{EVENT.RECOVERY.TIME}","date":"{EVENT.RECOVERY.DATE}"},"update":{"action":"{EVENT.UPDATE.ACTION}","date":"{EVENT.UPDATE.DATE}","time":"{EVENT.UPDATE.TIME}","message":"{EVENT.UPDATE.MESSAGE}"},"duration":"{EVENT.DURATION}","status":"{EVENT.STATUS}","age":"{EVENT.AGE}","ack":{"status":"{EVENT.ACK.STATUS}"}},"host":{"name":"{HOST.NAME}"},"trigger":{"url":"{TRIGGER.URL}"},"user":{"fullname":"{USER.FULLNAME}"}}

## License
To be announced, probably something like CC-BY... or buy me a drink
