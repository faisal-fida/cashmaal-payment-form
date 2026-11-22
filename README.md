# cashmaal-payment-form

A minimal Flask app that shows a payment form and forwards the submitted fields to the Cash-Maal payment gateway.

## Status

Demo quality. It is a single-file prototype: the form values are hard-coded in the template (placeholder email, URLs, order id), there is no validation, no order storage and no signature or callback handling. It also forwards the incoming request headers to the gateway and returns the gateway response body as-is. Do not use it in production as it is.

## Features

- One page (`/`) with a form: payment method, amount (100 or 200), currency (PKR or USD).
- On submit, builds a payload (`pay_method`, `amount`, `currency`, `success_url`, `cancel_url`, `client_email`, `web_id`, `order_id`, `addi_info`) and POSTs it to `https://www.cashmaal.com/Pay/`.
- Returns "Success! Response: ..." for HTTP 200 and "Error! Status Code: ..." otherwise.

## Tech stack

Python, Flask, Requests.

## Structure

```
app.py               Flask app and the POST to the gateway
templates/index.html Payment form
requirements.txt
```

## Setup and run

Requirements: Python 3.9+.

```sh
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
python app.py        # http://127.0.0.1:5000, debug mode on
```

No environment variables are used. To make it real you need to replace the hidden form values in `templates/index.html` (`web_id`, `order_id`, `client_email`, `success_url`, `cancel_url`) with your own Cash-Maal merchant details.

## Usage

Open `http://127.0.0.1:5000/`, pick the options and press "Pay With Cash-Maal". The gateway reply is shown as plain text.

## Limitations

- Debug mode is enabled in `app.py`; turn it off for any deployment.
- Prints request headers to the console.
- Untested against a live merchant account.

## License

MIT, see `LICENSE`.
