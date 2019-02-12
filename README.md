# Kesem.io SDK - Technical Documentation

The purpose of this SDK is to provide a rapid solution for developers looking to develop custom cryptocurrency wallets and/or dApps.

<q><strong>In Buidl we trust</strong></q>

# Starting app
## UnlockKesemData() API Call
Unlock Kesem backend db.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>Not used.</dd>
</dl>

## SecurityCheck()  API Call
Perform security check of the application environment. Check for malwares, rooting, etc… This API call should be called after UnlockKesemData().
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
## PostRegistrationRequest(phone, email = "") API Call
Creates a record for user on Kesem server. Kesem will send back to user SMS code by phone.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception</dd>
  <dt>result[0]</dt>
  <dd>"ok" for success.</dd>
  <dd>"error" to indicate error. Result[1] will have the error. In case of "Security violation", default Kesem wallet redirects user to security error screen and exit application afterwards.</dd>
</dl>

## ValidateSms(smscode) API Call
This function checks that SMS code is correct by verifing it with backend server. It is used during user registration process.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>"ok" for success.</dd>
  <dd>Otherwise - invalid code.</dd>
</dl>

# Information retreaval

## GetUuidHash() API Call
This function returns user-id in hash format to be used by external systems. For example as part of utm tokens or for tracking with external analytics systems.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>User hash.</dd>
</dl>

## GetEnvironment() API Call
Kesem is using multiple backend systems for testing and for production. It can be production, or development.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd><strong>production</strong> or <strong>development</strong> value</dd>
</dl>

## IsRegistered() API Call
This function return boolean value that indicate that user is registered, meaning:
* User accepted terms of service.
* User provided his phone number.
* User send correct SMS code.
* API backend finished init of the transaction database on the mobile phone.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd><strong>True</strong> / <strong>False</strong> to indicate registered user.</dd>
</dl>

# Login and basic security

## CanUseFingerprint() API Call
Check if the mobile device has fingerprint hardware support and it can be used.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd><strong>True</strong> / <strong>False</strong> to indicate that fingerprint can be used.</dd>
</dl>

## IsFingerprintSet() API Call
Check if application password is encrypted with fingerprint.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd><strong>True</strong> / <strong>False</strong> to indicate that password is encrypted with fingerprint code.</dd>
</dl>

## DecryptWithFingerprint() API Call
This function shows a popup screen asking user to provide fingerprint. This API call returns user password.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>Return application' user password in clear text.</dd>
</dl>

## CheckPassword(password) API Call
This function checks if user password is correct. Default Kesem Wallet ask performs user password check before showing user wallet balance.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception. Indicated bad password</dd>
  <dt>result[0]</dt>
  <dd>Not used.</dd>
</dl>

## ReplacePassword(oldpassword, newpassword) API Call
This functions is in charge to change user password.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>Not used.</dd>
</dl>


# Advanced Security

## RequestLocationPermission() API Call
This API call shows to user system popup to give application access to location permission if it is not already given. This is an optional step. It is recommended to enable lcoation tracking only if user has meaningful amount of crypto currencies on his account.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>Not used.</dd>
</dl>

## RemoveBackupSeed() API Call
This function removes second backup key seed for the database. It is done to improve security. In default Kesem app, user needs to confirm seed delation.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>Not used.</dd>
</dl>

## GetBackupSeed() API Call
Returns backup seed in hex format to the user to be used to be backuped.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>Backup seed.</dd>
</dl>

## IsBackupSeedSaved() API Call
This function check if database has no backup seed - meaning it was already backuped.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd><strong>True</strong> / <strong>False</strong> to indicate that backup was saved.</dd>
</dl>


# Wallet related API commands

## SyncTransactions() API Call
This API call check Kesem server for all new user transactions for all supported coins at once.

### Returns: nothing.

## CreateNewWallet(coinShortName, password) API Call
Create wallet for user. User can create just one wallet for specific coin. Password is required only for first wallet command.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd><strong>True</strong> / <strong>False</strong> to indicate that wallet was created.</dd>
</dl>

## GetUserWalletsData() API Call
This function returns JSON with all user wallets information.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>All user wallets info in JSON format.</dd>
</dl>

### Example:
```
[ { coinDetails: { coinCode: 1, shortName: 'BTC', title: 'BitCoin' }, 
      confirmedBalance: 0, unconfirmedBalance: 0 } ]
```

## GetSupportedWalletsTypes() API Call
Returns a JSON with a list of supported wallets the system can create for user. For example BTC, ETC, XTN, etc..
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dt>A list of supported wallets in JSON format.</dt>
</dl>

### Example:
```
[ { coinCode: 0, shortName: 'XTN', title: 'BitCoinTest' },
  { coinCode: 1, shortName: 'BTC', title: 'BitCoin' },
  { coinCode: 2, shortName: 'ETH', title: 'Ethereum' } ]
```

## ChallengeSms(smscode) API Call
This function checks that SMS code is correct by connection the backend server. It is used as a part of the user security challenge validation when user is sending funds out. For example if the sum of transaction is big.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>"ok" for success.</dd>
  <dd>Otherwise - invalid code.</dd>
</dl>

# Wallet Object Operations

## OpenWallet(coinShortName) API Call
Perform internal operation to open specific wallet. After opening the wallet, the following API calls can be used: GetAddress(), IsValidAddress(), RefreshAddress(), GetBalance(), SendCoins(), GetTransactiosData(). No need to run OpenWallet several time, only when you change active wallet.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>Not used.</dd>
</dl>

## GetAddress() API Call
Get current address of the wallet previously opened with OpenWallet()
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>Wallet address.</dd>
</dl>

## IsValidAddress() API Call
This API all checks that the arbitrary wallet address has correct formation. It is used as part of sanity check when sending out funds. Wallet should be opened state when calling this API call.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd><strong>True</strong> / <strong>False</strong> to indicate that address has correct format.</dd>
</dl>

## RefreshAddress() API Call
Refreshes wallet address with Kesem server and returns a new address. Wallet should be in opened state when calling this API call.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>New wallet address.</dd>
</dl>

## GetBalance() API Call
Returns balance of the current wallet opened with OpenWallet() API call.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>Confirmed balance.</dd>
  <dt>result[1]</dt>
  <dd>Unconfirmed balance.<dd>
</dl>


## SendCoins(amount, address, fee, password) API Call
Creates a transaction and sends it to Kesem server. Wallet should be in opened state when calling this API call.
### Parameters:
* Amount - sum of coins to send.
* Address - destination address to send
* Fee - mining fees to pay - X coins for 1000 bytes of transactions.
* Password - user wallet password.

## GetTransactionsData() API Call
Returns a list of all user transactions for current wallet.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>A list of transactions JSON format.</dd>
</dl>

### Example:
```
[ { timestamp: 1549287849,
                     remark: '',
                     confirmInBlock: 1455569,
                     transactionID: '4a28a9aa7d4c17cf4c9d8fc47ff41ca82828395853c1896e1397a7d4768ba9f0',
                     confirmations: 1,
                     amountInCryptoCurrency: 0.11907588,
                     amountInDollars: 0 } ]

```
