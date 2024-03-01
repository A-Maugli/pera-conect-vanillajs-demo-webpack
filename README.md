# Pack @perawallet/connect

Pack @perawallet/connect Node.js module as a standalone JavaScript library, using webpack. 

Test the packed library by a minimal test and a simple demo app.

## Config file
`webpack.config.js` and `tsconfig.json`

## package scripts
```
npm run clean	# clean up files
npm run build	# pack @perawallet/connect, output in ./dist/browser
npm run serve	# test the packed library
npm run comp_sri # compute SRI for ./dist/browser/perawalletconnect.min.js
```

## Issues
During `npm run build` you will get these warnings:
```
npm WARN deprecated @walletconnect/types@1.8.0: WalletConnect's v1 SDKs are now deprecated. Please upgrade to a v2 SDK. For details see: https://docs.walletconnect.com/
npm WARN deprecated @walletconnect/client@1.8.0: WalletConnect's v1 SDKs are now deprecated. Please upgrade to a v2 SDK. For details see: https://docs.walletconnect.com/
```

You can compute SRI (Sub Resource Integrity) for normal (not packed) js files ./public/perawalletconnect_demo.js, but the file should be saved with CRLF terminator,
as the browser converts LF to CRLF before computing its own SRI checksum.
See also https://github.com/kubernetes/website/issues/25414, "Failed to find a valid digest in the 'integrity' attribute for resource js/jquery-3.3.1.min.js with computed SHA-256 integrity"

The addEventListeners() in ./public/index.html should be be put into "$(document).ready", i.e. we should wait till DOM is ready.

In test.html, the reference to pwc, the packed PeraWalletConnect should be done in window.onload

## Generate the packed @perawallet/connect 
```
npm run clean
npm run build
npm run comp_sri
```

## Running the tests
```
npm -i -g serve
serve ./public
```

To run the test, enter `http://localhost:3000/test.html` in a browser url.

To run the demo, enter `http://localhost:3000/` in a browser url.