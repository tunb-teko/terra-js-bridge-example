# TERRA JS EXAMPLE

This project illustrates the usage of Terra in a mini-app written in JS (web, react native).

Currently, this project only contains an example of a static web app.

# Static web

## Running app

### Starting the static web

To running a static web app, we need to create a local server for serving the static files. For simple, we can use `Web Server for Chrome` for web server.

- Install `Web Server for Chrome` extension at [web-server-for-chrome](https://chrome.google.com/webstore/detail/web-server-for-chrome/ofhbbkphhbklhfoeikjpcbhemlocgigb)
- Run `Web Server for Chrome`, choose [web-static](/js-apps/static-web) folder and start server.

# Billing

## Running on the Super app

- Install [Android Super app](https://drive.google.com/file/d/1watzNg0e-69CMGBDskevyFdhGCpEhWnF/view?usp=sharing) to device or emulator.

- Set up to run `http://localhost:3000` on device or simualor: https://developer.chrome.com/docs/devtools/remote-debugging/local-server/
- Start app, click `Open billing app` button.

## Features

Check out more details at [static web example](/js-apps/static-web/index.html).

### [Billing] Paying for a bill

```html
<body>
  <!-- Insert these scripts at the bottom of the HTML, but before you use BillingKit -->

  <script src="https://unpkg.com/@terra-js/web-bridge@0.0.3/bundle/web-bridge.js"></script>
  <script src="https://unpkg.com/@terra-js/billing-kit@0.1.0-alpha.5/bundle/billing-kit.js"></script>

  <!-- Previously loaded Billing SDK -->
  <script>
    function onPayForBill() {
      const billingRequest = {
        creditAmount: 2873000,
        customerName: 'TRAN THI MINH VIEN',
        address: '4 TONG 1 NGAN',
        monthlyFee: '',
        addData: '[30062 03/2019 1180000][30062 04/2019 1693000]',
        agenCode: 'PHONGVUDEMO',
        svcCode: 'WATER-BILL',
        customerCode: '30062',
        providerCode: 'NUOC_TRANOC',
        providerName: 'Cấp nước Trà Nóc',
        mobileNumber: '',
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

### [Billing] Showing transactions history screen

```html
<body>
  <!-- Insert these scripts at the bottom of the HTML, but before you use BillingKit -->

  <script src="https://unpkg.com/@terra-js/web-bridge@0.0.3/bundle/web-bridge.js"></script>
  <script src="https://unpkg.com/@terra-js/billing-kit@0.1.0-alpha.5/bundle/billing-kit.js"></script>

  <!-- Previously loaded Billing SDK -->
  <script>
    function openTransactionsHistory() {
      billingKit.showTransactionsHistory();
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
