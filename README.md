# Kesem.io SDK - Technical Documentation

The purpose of this SDK is to provide a rapid solution for developers looking to develop custom cryptocurrency wallets and/or dapps.

*In Buidl we trust*

# Starting app
## UnlockKesemData()
Unlock Kesem backend db.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>Not used.</dd>
</dl>

## SecurityCheck()
Perform security check of the application environment. Check for malwares, rooting, etc… This should be called after UnlockKesemData().
### Returns:
<dl>
  <dt>error</dt>
  <dd>If contains "Old version" redirect user to Update version screen and stops app execution afterwards.</dd>
  <dd>If contains "connection timeout" redirect user to no Internet error screen and stops app afterwards.</dd>
  <dd>If contains "Security violation" redirect use to security error screen and stops app afterwards.</dd>
  <dt>result[0]</dt>
  <dd>Not used.</dd>
 </dl>

# Register app
## PostRegistrationRequest(phone, email =””)
Creates a record for user on Kesem server. Kesem will send back to user SMS code.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception</dd>
  <dt>result[0]</dt>
  <dd>"ok" for success.</dd>
  <dd>"error" to indicate error. Result[1] will have the error. In case of "Security violation" redirect the use ro security error screen and exit application afterwards.</dd>
</dl>

