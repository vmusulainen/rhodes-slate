# Rho.Barcode

The Barcode Module provides access to control the functionality of the device's scanner. Because RhoMobile Suite is designed to run on both Consumer devices and Symbol Technologies' enterprise devices support for the Barcode API will vary for each method and properties depending on which platform you are running on. Please note that a lot these APIs are optimized for the extended functionality that Symbol Technologies devices provide. Check the platform indicators in each property or method section. In general if you are developing for a consumer device the number of symbologies available to you will be limited to just the most common ones, eg EAN13, UPCA etc and your scanning will be via the device camera. If your application is running on Symbol Technologies' hardware you will have much finer control over a more fully featured Scanner, often with a choice of scanner hardware on the device. In general if you wish to capture a single barcode in a 'one shot' use case, eg your App just wants to capture a single barcode to be submitted to a price comparison website then use Barcode.take(callback); if your application is expecting a number of barcodes to be received, common in enterprise scenarios for example a user in a warehouse then use Barcode.enable(callback). The Barcode API will not run on non-Symbol Technologies Windows Mobile / CE devices.Only the foreground application is given access to the scanning hardware, when an application is sent to the background its state will be saved and it will automatically relinquish control of the scanner. When brought back to the foreground, an application previously using the barcode API will have its previous configuration reapplied automatically.In VC70 scanner will work only if connected in SSI Mode. In  Symbol android devices, it is recommended to use EMDK for KitKat devices and not to use EMDK in JellyBean devices.

## Enabling the API
In order to use this API you must include the following extension in your `build.yml`

`
extensions: ["barcode"]
`

<aside class="warning">
If you are building a Windows Mobile or Windows CE app with this API, you must set your app_type as "rhoelements" in your build.yml as shown [here](../guide/build_config#other-build-time-settings).
</aside>

<aside class="notice">
Be sure to review the [JavaScript API Usage](/guide/api_js) guide for important information about using this API in JavaScript
</aside>

<aside class="notice">
Be sure to review the [Ruby API Usage](/guide/api_ruby) guide for important information about using this API in Ruby
</aside>

## enumerate
```ruby
# get all barcode scanners
scanners = Rho::Barcode.enumerate

# find scanner by identifier
scanner = Rho::Barcode.enumerate.find {|each| each.identifier == aString}
```

```javascript
// get all barcode scanners
var scanners = Rho.Barcode.enumerate

// find scaner by identifier
var scanner = Rho.Barcode.enumerate().find(function(each) {
  return each.identifier == aString;
})
```

languages: `javascript`, `ruby`

platforms: `android`, `ios`, `windows`

Used to gain access to all scanner objects present on the device. For consumer devices you will most likely only have a single scanner, your device's camera but Enterprise grade hardware may have two or more scanners attached.

**Parameters**

No Parameters

## take

```ruby
def scan_using_default_scanner
  # Scan with default options
  Rho::Barcode.take({}, url_for(:action => :scan_received))
end

def scan_received
  # Did we actually find a barcode ?
  # If status is not 'ok', the scan was canceled
  if @params["status"] == "ok"
    Rho::Log.info(@params["barcode"],"Barcode result")
  else
    Rho::Log.info("canceled", "Barcode result")
  end
end
```

```javascript
function scanUsingDefaultScanner(){
  // Scan with default options
  Rho.Barcode.take({}, scanCallback);
}

function scanCallback(data){
  // Did we actually find a barcode ?
  // If status is not 'ok', the scan was canceled

    if (data["status"]=="ok") {
        alert('Barcode scanning complete. Scanned barcode: '+data["barcode"]);
    } else {
        alert('Barcode scanning aborted');
    }
    Rho.Barcode.stop();
}
```

> The above command returns to callback JSON structured like this:

```json
{
  "barcode": "1234567890",
  "status": "ok"
}
```
languages: `javascript`, `ruby`

platforms: `android`, `ios`, `windows`

Enable the scanner and start capturing the barcode automatically. On Symbol Technologies' devices the amount of time to scan the barcode is defined by the scanTimeout property. On iPhone and Android if a barcode is found, the user can confirm barcode recognition, or continue to try to recognize the barcode. When the user confirms or cancels, the callback is called. Once the callback has been called the barcode hardware is disabled.This method will work only on scanners which support soft scan.

