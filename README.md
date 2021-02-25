# hubitat_flume

This provides a driver integration for Flume water monitoring devices.  

Note that all operations have a cloud (internet) interaction.  The API accesses are made according to the Flume Personal API reference:
* https://help.flumewater.com/en/articles/3108017-flume-personal-api

Special thanks to @jpalovick for their testing and feedback.

# Manual Installation instructions:

* In the *Drivers Code* section of Hubitat, add the flumeDevice driver.
* In the *Devices* section of Hubitat, add a *New Virtual Device* of type Flume Device
* Gather your Client ID and Client Secret from the Flume portal, under API Access:  https://portal.flumewater.com/settings
* On the configuration page for the newly created *Device*, enter these details and then Save Preferences:
    * Client ID, Client Secret, username, and password
    * The refresh interval in minutes
        * Note that there is a documented limit of 120 API accesses per hour, and each device refresh or action is at least one access.  Set this number accordingly.
    * Choose your preferred option for the *Use sliding time windows* option
        * If set to disabled, the data will be similar to the Flume app reporting which are aligned to specific days or dates as the start of the time period (e.g. Monday as start of the current week; first day of calendar month; first minute of the current hour)
        * If enabled, the time periods will represent a sliding window from the time of query.  Examples: last hour is the 60 minutes preceding the time of query; last month is the 30 days preceding the time of query

# Usage instructions:

* On each driver *refresh*, all of the usage details are updated.  Also, usage alerts are queried and logged as described here:
    * For usage alerts related to normal conditions (e.g. "High Flow" usage alert), the full alert text is logged via an entry in the *alertStream* attribute.
    * For Flume Smart Leak alerts, the *water* attribute will be marked wet.  Once you have handled this event accordingly, clear the condition with the *clearWetStatus* custom command on the device.
    * The *presence* attribute will reflect the status of away_mode for the system.
    
# Disclaimer

I have no affiliation with any of the companies mentioned in this readme or in the code.
