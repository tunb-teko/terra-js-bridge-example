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

Check out more details at [static web example](/js-apps/static-web/index.html).

### Paying for a bill

```html
<body>
  <!-- Insert these scripts at the bottom of the HTML, but before you use BillingKit -->

  <script src="https://unpkg.com/@terra-js/web-bridge@0.0.3/bundle/web-bridge.js"></script>
  <script src="https://unpkg.com/@terra-js/billing-kit@0.1.0-alpha.1/bundle/billing-kit.js"></script>

  <!-- Previously loaded Billing SDK -->
  <script>
    function onPayForBill() {
      const billingRequest = {
        respCode: 'respCode',
        trace: 'trace',
        serviceCode: '000010',
        providerCode: '196000',
        customerCode: 'PB17010000002',
        senderInfo: 'PB17010000002',
        bankCode: '950012',
        channel: '6015',
        accountNo: '',
        amount: 10000,
        customerName: 'CustomerName',
        address: 'Address',
        monthlyFee: '[17 2/2013 719000][17414437 2/2013 1000000]',
        addData: undefined,
        vnpayDateTime: '20210623110126',
        localDateTime: '20210623105143',
        sign: 'sign',
      };
      const paymentOptions = {
        shouldShowPaymentResultScreen: true,
      };

      billingKit.payForBill(billingRequest, paymentOptions).then((result) => {
        switch (result.resultCode) {
          case 'succeeded':
            // go to the home page or do something else
            break;
          case 'failed':
            // ignore 'ProcessOrderFail' error
            if (result.error.code != 'ProcessOrderFail') {
              // go to the home page or do something else
            }
            break;
          case 'canceled':
            // should ignore 'canceled' result
            break;
          default:
          // should ignore unhandled result
        }
      });
    }
  </script>
</body>
```

### Finishing the web app

```html
<body>
  <!-- Insert these scripts at the bottom of the HTML, but before you use TerraKit -->

  <script src="https://unpkg.com/@terra-js/web-bridge@0.1.0-alpha.5/bundle/web-bridge.js"></script>
  <script src="https://unpkg.com/@terra-js/terra-kit@0.1.0-alpha.4/bundle/terra.js"></script>

  <!-- Previously loaded TerraKit SDK -->
  <script>
    function onFinish() {
      terraKit.finish();
    }
  </script>
</body>
```
