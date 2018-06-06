# Rho.WebView

* %p - platform name ("Windows CE " + version number)
* %w - WebKit version number
* %e - WebKit version number.

Use the UserAgent setting to spoof your device to the server, e.g. to view content designed for the desktop on your mobile screen.
From RhoElements 2.1 onwards the default value was changed to work out of the box with a greater number of server configurations, prior to RhoElements 2.1 the default user agent was: "Mozilla/5.0 (%p) AppleWebKit/%w (KHTML, like Gecko) WebKit/%e Safari/%w"
                

If you open your page in WebView, and after it makes a few jumps by linking (for example, to outside web adresses for example), currentLocation will still return the initial url opened in WebView. Also, if you use JQMobile, current_location has the initial URL, but does not reflect the actual window.location containing the JQMobile additional address by adding #, etc. See currentUrl.

For most mobile platforms, WebView.execute_js has been implemented via redirection to URL with 'javascript:' schema. If WebView.execute_js used in an AJAX call handler method in the controller, it may lead to the situation where the success javascript handler will never be executed. This may happen because, at the moment of success handler should be executed, a URL of the page already has been changed. This means no handlers from the previous page are valid.