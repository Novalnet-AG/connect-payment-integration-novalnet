# Novalnet Payments Connector for commercetools — Installation Guide

**Version:** 1.0.0  
**Release date:** 11 November 2026  
**Release notes:** New release of the Novalnet payment connector, providing an integrated payment experience and improved features and usability.

This guide explains how to install, configure, test, operate, and uninstall the Novalnet Payments Connector for commercetools.

## Contents

- [1. Quick setup](#1-quick-setup)
  - [1.1. Connector installation](#11-connector-installation)
  - [1.2. Global configuration](#12-global-configuration)
    - [1.2.1. Client key and allowed domains](#121-client-key-and-allowed-domains)
    - [1.2.2. Notification and webhook configuration](#122-notification-and-webhook-configuration)
  - [1.3. Activate payment methods in the Novalnet Admin Portal](#13-activate-payment-methods-in-the-novalnet-admin-portal)
  - [1.4. Activate payment methods in commercetools](#14-activate-payment-methods-in-commercetools)
    - [1.4.1. Checkout application overview](#141-checkout-application-overview)
    - [1.4.2. Payment integrations](#142-payment-integrations)
- [2. Testing and going live](#2-testing-and-going-live)
- [3. Additional configuration](#3-additional-configuration)
  - [3.1. Settings for payment methods](#31-settings-for-payment-methods)
  - [3.2. Credit and debit card settings](#32-credit-and-debit-card-settings)
- [4. Managing payments in commercetools](#4-managing-payments-in-commercetools)
  - [4.1. Order management](#41-order-management)
  - [4.2. Transaction overview](#42-transaction-overview)
  - [4.3. Generate a bearer token](#43-generate-a-bearer-token)
  - [4.4. Capture or cancel a transaction](#44-capture-or-cancel-a-transaction)
  - [4.5. Refund an order](#45-refund-an-order)
- [5. Uninstallation](#5-uninstallation)
  - [5.1. Deactivate and delete payment methods](#51-deactivate-and-delete-payment-methods)
  - [5.2. Uninstall the Novalnet connector](#52-uninstall-the-novalnet-connector)
- [6. Novalnet technical support](#6-novalnet-technical-support)

## 1. Quick setup

A Novalnet merchant account is required before you can begin accepting payments. If you do not have a merchant account, contact [sales@novalnet.de](mailto:sales@novalnet.de).

Before starting, ensure you can sign in to both the [Novalnet Admin Portal](https://admin.novalnet.de/) and your commercetools Merchant Center.

### 1.1. Connector installation

1. Sign in to the **commercetools Merchant Center**. Open your profile menu and select **Manage organizations & teams**.

2. Select the organization in which you want to install the connector.

3. Navigate to **Connect**, search for the **Novalnet Payments** connector, and click **Install**.

4. On the commercetools connector configuration page, select the required **Region**, **Organization** (selected by default), **Deployment environment**, and **Projects**. Click **Next**.

5. The **Novalnet Payments** configuration page opens. Complete the global settings in the next section before finishing installation.

### 1.2. Global configuration

The connector requires the following credentials from the Novalnet Admin Portal:

| Credential | Where to obtain it |
| --- | --- |
| Product activation key | Novalnet project → **API credentials** |
| Tariff ID / Tariff Key | Novalnet project → **API credentials** |
| Client Key | Novalnet project → **API credentials** |
| Payment access key | Novalnet project → **API credentials** |

1. In the [Novalnet Admin Portal](https://admin.novalnet.de/), open **Projects** and click the view icon for the relevant project.

2. Select **API credentials** and copy the **Product activation key**, **Tariff ID**, **Client Key**, and **Payment access key**.

3. Paste these values into the corresponding fields on the commercetools connector configuration page. Click **Install** to save the configuration and install the connector.

#### 1.2.1. Client key and allowed domains

The Client Key identifies your Novalnet merchant account for client-side requests. It is used to display the secure payment form and to temporarily tokenize sensitive payment information.

> **Important:** Novalnet accepts client-side requests only from domains allowlisted for the corresponding project. Your website must use a valid, secure `https://` URL.

1. Open the [Novalnet Admin Portal](https://admin.novalnet.de/).
2. Navigate to **Projects** and open the required project.

3. Open the **API credentials** tab and select the control beside **Allowed Domain(s)**.

4. Enter your website URL in the **Domain name** field and click **+ Add**.

5. Confirm that the domain appears under **Allowed Domain(s)**.

#### 1.2.2. Notification and webhook configuration

The connector provides a configuration setting for manually testing Novalnet notifications/webhooks.

| Setting | Value | Behavior |
| --- | --- | --- |
| `NOVALNET_WEBHOOK_TEST_MODE` | `1` | Allows manual testing of the Novalnet notification/webhook. |
| `NOVALNET_WEBHOOK_TEST_MODE` | `0` | Disables the manual test mode; use this value before going live. |

> **Important:** Set `NOVALNET_WEBHOOK_TEST_MODE` to `0` before switching to live mode to prevent unauthorized calls from external parties, as instructed in the original installation guide.

### 1.3. Activate payment methods in the Novalnet Admin Portal

Available Novalnet payment methods are described on the [Novalnet payment methods page](https://www.novalnet.com/payment). For additional payment method requests, contact [sales@novalnet.de](mailto:sales@novalnet.de).

1. In the [Novalnet Admin Portal](https://admin.novalnet.de/), go to **Projects**, choose your project, and open **Payment Methods**. Click **Edit Payment Methods**.

2. Select the payment methods you want to offer and click **Update**.

3. **PayPal:** If you want to accept PayPal, configure its API credentials in the Novalnet Admin Portal.

   Enter the required PayPal credential details and click **Confirm**.

4. **PostFinance:** If you want to accept PostFinance, configure the **Ep2-Merchant ID** in the Novalnet Admin Portal.

### 1.4. Activate payment methods in commercetools

To display Novalnet payment methods in the storefront, you must also add and activate each required payment method in the commercetools Merchant Center.

#### 1.4.1. Checkout application overview

1. Sign in to the **commercetools Merchant Center** and navigate to **Checkout → Overview**.

2. Under **List of applications**, select the Checkout application you want to configure.

#### 1.4.2. Payment integrations

1. Open **Payment integrations** and click **Add payment integration**.

2. Under connector selection, choose **Novalnet Payments** from the **Payment connectors** dropdown.

3. Under payment integration setup, select the required Novalnet **Payment method** and enter a **Payment integration name**.

4. Under **Customization of the payment method display**, provide the **Payment method name** to show on the storefront.

5. Download the payment method icon from the GitHub repository referenced in your connector distribution, host it on your server, and enter the hosted URL in **Payment method icon URL**.

6. Click **Save** to add the payment integration. Open its configuration and change the **Status** toggle to **Activated**.

Repeat these steps for each Novalnet payment method you intend to make available at checkout. For payment-specific settings, see [Additional configuration](#3-additional-configuration).

## 2. Testing and going live

To perform test transactions:

1. Sign in to the Merchant Center and open your organization's connector area (see [Connector installation](#11-connector-installation)).
2. Navigate to **Connect → Manage connectors**.

3. Open **Installations** and select the installed **Novalnet Payments** connector.

4. Under **Apps**, select **processor**. Set the applicable test mode setting (for example, `NOVALNET_PAYMENT_TEST_MODE`) to `1`, and click **Redeploy**. A confirmation dialog asks you to reinstall the connector to deploy the changes.

5. Click **Reinstall** to deploy the new configuration.

In test mode, Novalnet does not charge a real transaction amount. You can use [Novalnet test payment data](https://developer.novalnet.com/testing/) to place test orders.

### Switch to live mode

1. Change the applicable payment test mode configuration value from `1` to `0` for live transactions.
2. Save the individual payment configurations again in the shop administration panel to update their settings.
3. Ensure `NOVALNET_WEBHOOK_TEST_MODE` is set to `0` as explained in [Webhook configuration](#122-notification-and-webhook-configuration).

> **Note:** Configuration changes to the processor are deployed using **Redeploy** and the subsequent **Reinstall** confirmation, as described above.

## 3. Additional configuration

### 3.1. Settings for payment methods

To configure individual payment methods, navigate to **Connect → Manage connectors → Installations → Novalnet Payments → processor**, then find the relevant payment method settings.

#### Payment action: debit immediately or reserve funds for later

This option is available for:

- Credit/Debit Cards
- Direct Debit SEPA
- Direct Debit SEPA with payment guarantee
- Invoice
- Invoice with payment guarantee
- PayPal

Two payment actions are supported:

| Payment action | Description |
| --- | --- |
| **Capture** (`payment`) | Executes payment immediately when the buyer places an order. This is the default. An empty configuration value is treated as Capture. |
| **Authorize** (`authorize`) | Verifies the payment details and reserves funds for capture at a later point. |

**Minimum transaction amount for authorization:** Payments from the specified amount are authorized (reserved) rather than captured immediately. Leave this field blank to authorize all transactions when authorization is configured.

#### Payment due date (in days)

The `NOVALNET_[PAYMENT]_DUE_DATE` setting determines the number of days given to a buyer to complete a payment. This option is available for **Direct Debit SEPA**, **Invoice**, and **Prepayment**.

| Payment method | Allowed value / behavior |
| --- | --- |
| Direct Debit SEPA | Number of days before the payment is debited: **3–14 days**. |
| Invoice | Buyer transfer period: **more than 7 days**. If blank, defaults to **14 days**. |
| Prepayment | Buyer transfer period: **7–28 days**. If blank, defaults to **14 days**. |

#### Payment guarantee

Payment guarantee options are available for **Direct Debit SEPA with payment guarantee** and **Invoice with payment guarantee**, subject to the applicable guarantee requirements. For more information, see [Novalnet payment guarantee](https://developer.novalnet.com/onlinepayments/aboutguarantee).

##### Force non-guarantee payment

Set the corresponding **Force Non-Guarantee payment** option to `1` to allow the payment to proceed as a non-guaranteed payment when guarantee requirements are not met.

> **Important:** If this option is enabled, activate both **Direct Debit SEPA** and **Invoice** payment methods in the Novalnet Admin Portal, as required by the source guide.

##### Allow B2B customers

The setting `NOVALNET_GUARANTEED_[PAYMENT]_ALLOW_B2B_CUSTOMERS` controls whether B2B buyers can use the guarantee-based payment method.

Set the value to `1` to allow B2B customers.

### 3.2. Credit and debit card settings

#### Enforce 3-D Secure for cards issued outside the EU

Enable **Enforce 3D secure on payment outside EU** to require authentication using **3DS 2.0 SCA** for cards issued outside the European Union.

## 4. Managing payments in commercetools

### 4.1. Order management

In the commercetools Merchant Center, navigate to **Orders → Order list** to view and manage orders.

### 4.2. Transaction overview

1. Select an order from the list to view its payment information and Novalnet transaction details.

2. Open the order's **Payments** section. In **Transactions**, click **View custom fields**.

3. The Novalnet payment and transaction details are displayed in the custom-fields view.

### 4.3. Generate a bearer token

To perform payment actions, such as **capture**, **cancel**, or **refund**, you need a valid commercetools OAuth bearer token.

1. Execute the following command in a terminal, replacing the placeholders with your project credentials:

   ```bash
   curl "https://{auth_host}/oauth/token" -X POST \
     --basic --user "{clientId}:{clientSecret}" \
     -d "grant_type=client_credentials&scope=manage_project:{projectKey}"
   ```

2. Replace the placeholders with the following values:

   | Placeholder | Description |
   | --- | --- |
   | `{auth_host}` | commercetools OAuth authentication host for your project's region. |
   | `{clientId}` | commercetools API Client ID. |
   | `{clientSecret}` | commercetools API Client Secret. |
   | `{projectKey}` | commercetools Project Key. |

3. Read the `access_token` field from the OAuth response and use that value as the bearer token in subsequent requests.

> **Note:** Bearer tokens expire. Generate a new token after the current token expires.

### 4.4. Capture or cancel a transaction

If the configured payment action is **Authorize**, the transaction is initially placed in the **Authorization** state, with the funds reserved for later capture or cancellation.

The source guide lists Credit/Debit Cards, Direct Debit SEPA, Direct Debit ACH, Direct Debit SEPA with payment guarantee, Invoice with payment guarantee, and PayPal as payment methods that may have an Authorization status according to their payment action.

#### Capture an authorized transaction

Use the [bearer token](#43-generate-a-bearer-token) to request capture of an authorized payment:

```bash
curl "https://checkout.{region}.commercetools.com/{projectKey}/payment-intents/{paymentId}" -i \
  --header "Authorization: Bearer ${BEARER_TOKEN}" \
  --header 'Content-Type: application/json' \
  --data-binary @- <<'DATA'
{
  "actions": [
    {
      "action": "capturePayment",
      "amount": {
        "centAmount": 100,
        "currencyCode": "EUR"
      },
      "merchantReference": "example-reference"
    }
  ]
}
DATA
```

When the request succeeds, Novalnet processes the capture.

#### Cancel an authorized transaction

To cancel an authorization:

```bash
curl "https://checkout.{region}.commercetools.com/{projectKey}/payment-intents/{paymentId}" -i \
  --header "Authorization: Bearer ${BEARER_TOKEN}" \
  --header 'Content-Type: application/json' \
  --data-binary @- <<'DATA'
{
  "actions": [
    {
      "action": "cancelPayment",
      "merchantReference": "example-reference"
    }
  ]
}
DATA
```

When the request succeeds, the authorization is canceled by Novalnet.

#### Capture and cancel parameters

| Parameter | Type in source guide | Description | Example |
| --- | --- | --- | --- |
| `action` | String | Payment intent action: `capturePayment` or `cancelPayment`. | `capturePayment` |
| `amount` | Object | Capture amount. The guide states it must equal the authorized amount. | `{"centAmount":100,"currencyCode":"EUR"}` |
| `centAmount` | String | Amount in the currency's smallest unit (shown as a JSON number in the request). | `100` |
| `currencyCode` | String | ISO 4217 currency code. | `EUR` |
| `merchantReference` | String | Merchant reference used to reconcile the payment intent action. | `INV-189757` |
| `paymentId` | String | Identifier of the commercetools Payment. | `8bdf9dd3-f07b-4d18-a0f2-507bac84c625` |
| `region` | String | Region hosting the Checkout application. | `europe` |
| `projectKey` | String | commercetools Project Key. | `Commercetools` |

To find the `paymentId`, open the relevant order. The **Payment ID** is displayed in its **Payments** section.

After capturing or canceling a transaction, you can see updated transaction information under **View custom fields**.

### 4.5. Refund an order

Novalnet supports full or partial refunds. To initiate a refund, submit the `refundPayment` action for the appropriate capture transaction.

```bash
curl "https://checkout.{region}.commercetools.com/{projectKey}/payment-intents/{paymentId}" -i \
  --header "Authorization: Bearer ${BEARER_TOKEN}" \
  --header 'Content-Type: application/json' \
  --data-binary @- <<'DATA'
{
  "actions": [
    {
      "action": "refundPayment",
      "amount": {
        "centAmount": 100,
        "currencyCode": "EUR"
      },
      "transactionId": "example-transactionId",
      "merchantReference": "example-reference"
    }
  ]
}
DATA
```

#### Refund parameters

| Parameter | Type in source guide | Description | Example |
| --- | --- | --- | --- |
| `action` | String | Payment intent action. | `refundPayment` |
| `amount` | Object | Amount to refund, fully or partially. | `{"centAmount":100,"currencyCode":"EUR"}` |
| `centAmount` | String | Amount in the currency's smallest unit (shown as a JSON number in the request). | `100` |
| `currencyCode` | String | ISO 4217 currency code. | `EUR` |
| `transactionId` | String | Identifier of the capture transaction to refund. | `e4ff0222-0aeb-41ca-bfdb-2e918a1315ff` |
| `merchantReference` | String | Merchant-defined reference for reconciliation. | `INV-872921` |
| `paymentId` | String | Identifier of the commercetools Payment. | `8bdf9dd3-f07b-4d18-a0f2-507bac84c625` |
| `region` | String | Region hosting the Checkout application. | `europe` |
| `projectKey` | String | commercetools Project Key. | `Commercetools` |

To find the `paymentId`, follow the instructions in [Capture or cancel a transaction](#44-capture-or-cancel-a-transaction).

To find the `transactionId`:

1. Open the applicable order and locate the **Transactions** table.
2. Select the **Transaction ID** of the transaction whose **Transaction Type** is **Charge**.

After the refund, the transaction history is updated and a new Novalnet transaction ID (TID) is displayed. See [Transaction overview](#42-transaction-overview) for more details.

## 5. Uninstallation

### 5.1. Deactivate and delete payment methods

Before removing the connector, deactivate and delete its payment integrations from the Checkout application.

1. In the Checkout application's **Payment integrations** section, select the Novalnet payment method to remove (for example, **Novalnet – Credit/Debit Cards**).

2. Switch **Status** off and confirm **Deactivate payment method** in the dialog.

3. Open the payment integration's actions menu and choose the delete option.

4. In the confirmation dialog, click **Delete payment method**.

Repeat for every Novalnet payment method in the Checkout application.

### 5.2. Uninstall the Novalnet connector

1. Return to the connector installation list by following [Testing and going live](#2-testing-and-going-live), steps 1–3.
2. Open the **Novalnet Payments** connector configuration and click **Uninstall**.

3. Confirm by clicking **Uninstall** in the confirmation dialog.

4. The interface displays **The uninstallation process has started**, and the connector status changes to **Uninstalling**.

When the operation completes, the Novalnet Payments Connector is uninstalled.

## 6. Novalnet technical support

For installation assistance or technical questions, contact:

- **Technical support:** [technic@novalnet.de](mailto:technic@novalnet.de), +49 89 9230683-19.
- **Merchant accounts, new connectors, and additional payment methods:** [sales@novalnet.de](mailto:sales@novalnet.de), +49 89 9230683-20.

For licensing, see the [Novalnet Freeware License Agreement](https://www.novalnet.com/payment-plugins-free-license/).

---

