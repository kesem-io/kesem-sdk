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
  <dd>"error" to indicate error. Result[1] will have the error. In case of "Security violation" redirect the user to security error screen and exit application afterwards.</dd>
</dl>

## ValidateSms(smscode)
This function checks that SMS code is correct by connecting the backend server. It is used during user registration process.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>"ok" for success.</dd>
  <dd>Otherwise - invalid code.</dd>
</dl>

# Information retreaval

## GetUuidHash()
This function returns user id in hash format to be used by external systems. For example as part of utm tokens or for tracking with external analytics systems.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>User hash.</dd>
</dl>

## GetEnvironment()
Kesem is using multiple backend systems for testing and for production. It can be production, or development.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>"production"/"development" value</dd>
</dl>

## IsRegistered()
This function return boolean value that indicated if user is registered, meaning:
User accepted terms of service.
User provided his phone number.
User send correct SMS code.
Backend performed finished init of the database.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd><strong>True</strong> / <strong>False</strong> to indicate registered user.</dd>
</dl>

# Login and basic security

## CanUseFingerprint()
Check if the device has support for fingerprints.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd><strong>True</strong> / <strong>False</strong> to indicate that fingerprint can be used.</dd>
</dl>

## IsFingerprintSet()
Check if application password is encoded with fingerprint.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd><strong>True</strong> / <strong>False</strong> to indicate that password is encrypted with fingerprint code.</dd>
</dl>

## DecryptWithFingerprint()
This function will show a popup asking him to provide fingerprint. It returns user password.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>Return application user password in clear text.</dd>
</dl>

## CheckPassword(password)
This function checks if user password is correct it the system can show to user wallet balance.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception. Indicated bad password</dd>
  <dt>result[0]</dt>
  <dd>Not used.</dd>
</dl>

## ReplacePassword(oldpassword, newpassword)
This functions is in charge to change user password.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>Not used.</dd>
</dl>


# Advanced Security

## RequestLocationPermission()
Shows to user system popup to give application access to location permission if it is not already given. This is an optional step and it is advised only if user has meaningful amount of money on his account.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>Not used.</dd>
</dl>

## RemoveBackupSeed()
This function removes second backup key seed for the db. It is done to improve security. In kesem app, user needs to confirm seed delation.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>Not used.</dd>
</dl>

## GetBackupSeed()
Returns backup seed in hex format to be backuped.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>Backup seed.</dd>
</dl>

## IsBackupSeedSaved()
This function check if database has no backup seed - meaning it was already exported.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd><strong>True</strong> / <strong>False</strong> to indicate that backup was saved.</dd>
</dl>


# Wallet related API commands

## SyncTransactions()
Check Kesem server for new transactions for all supported coins at once.

### Returns: nothing.

## CreateNewWallet(coinShortName, password)
Create wallet for user. User can create just one wallet for specific coin. Password is required only for first wallet command.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd><strong>True</strong> / <strong>False</strong> to indicate that wallet was created.</dd>
</dl>

## GetUserWalletsData()
This function returns JSON with all user wallets.
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

## GetSupportedWalletsTypes()
Returns a JSON with a list of supported wallets the system can create for user. For example BTC, ETC, XTN, etc..
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dt>A list of supported wallets info in JSON format.</dt>
</dl>

### Example:
```
[ { coinCode: 0, shortName: 'XTN', title: 'BitCoinTest' },
  { coinCode: 1, shortName: 'BTC', title: 'BitCoin' },
  { coinCode: 2, shortName: 'ETH', title: 'Ethereum' } ]
```

## ChallengeSms(smscode)
This function checks that SMS code is correct by connection the backend server. It is used as a part of the user security challenge when sending funds if the sum of transaction is big and also as part of wallet restoration in case wallet data was corrupted.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>"ok" for success.</dd>
  <dd>Otherwise - invalid code.</dd>
</dl>

# Wallet Object Operations

## OpenWallet(coinShortName)
Perform internal open of the wallet. After opening the wallet, the following API calls can be used: GetAddress(), IsValidAddress(), RefreshAddress(), GetBalance(), SendCoins(), GetTransactiosData(). No need to run OpenWallet several time, only when you change active wallet.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>Not used.</dd>
</dl>

## GetAddress()
Get current wallet address of the wallet previously opened with OpenWallet()
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>Wallet address.</dd>
</dl>

## IsValidAddress()
Check that the wallet address has correct formation. It is used to perfrom sanity check when sending out funds. It is required that wallet was opened with OpenWallet().
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd><strong>True</strong> / <strong>False</strong> to indicate that address has correct format.</dd>
</dl>

## RefreshAddress()
Refreshes wallet address with Kesem server and returns a new one. It is not supported for all currencies.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>New wallet address.</dd>
</dl>

## GetBalance()
Return balance of the current wallet opened with OpenWallet() API call.
### Returns:
<dl>
  <dt>error</dt>
  <dd>Error / exception.</dd>
  <dt>result[0]</dt>
  <dd>Confirmed balance.</dd>
  <dt>result[1]</dt>
  <dd>Unconfirmed balance.<dd>
</dl>


## SendCoins(amount, address, fee, password)
Creates a transaction and sends it to Kesem server.
### Parameters:
Amount - sum of coins to send.
Address - destination address to send
Fee - mining fees to pay - X coins for 1000 bytes of transactions.
Password - user wallet password.

## GetTransactionsData()
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
