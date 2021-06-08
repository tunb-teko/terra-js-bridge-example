# TERRA JS EXAMPLE

This project illustrates the usage of Terra in a mini-app written in JS (web, react native).

Currently, this project only contains an example of a static web app.

# Static web

## Running app

### Starting the static web

To running a static web app, we need to create a local server for serving the static files. For simple, we can use `Web Server for Chrome` for web server.

- Install `Web Server for Chrome` extension at [web-server-for-chrome](https://chrome.google.com/webstore/detail/web-server-for-chrome/ofhbbkphhbklhfoeikjpcbhemlocgigb)
- Run `Web Server for Chrome`, choose [web-static](/js-apps/static-web) folder and start server.

### Running on the Super app

- Install [Android Super app](https://drive.google.com/file/d/1watzNg0e-69CMGBDskevyFdhGCpEhWnF/view?usp=sharing) to device or emulator.

- Start app, click `Open web app` button and enter the url of the web app

## Features

### Payment

```html
<body>
  <!-- Insert these scripts at the bottom of the HTML, but before you use PaymentKit -->

  <script src="https://unpkg.com/@terra-js/web-bridge@0.0.1/bundle/web-bridge.js"></script>
  <script src="https://unpkg.com/@terra-js/payment-kit@0.0.1/bundle/payment-kit.js"></script>

  <!-- Previously loaded PaymentKit SDK -->
  <script>
    function onPay() {
      paymentKit
        .pay({
          merchantCode: 'MERCHANT_TEST',
          orderCode: 'order-code-123',
          amount: 10000,
          shouldShowPaymentResultScreen: false,
        })
        .then((result) => {
          switch (result.resultCode) {
            case 'succeeded':
              alert(`Payment succeeded: ${result.data.transactionCode}`);
              break;
            case 'failed':
              alert(`Payment failed: ${result.error.message}`);
              break;
            case 'canceled':
              alert(`Payment canceled`);
              break;
            default:
              alert(JSON.stringify(result));
          }
        });
    }
  </script>
</body>
```
