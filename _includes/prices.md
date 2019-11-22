{% assign hide-direct-debit = include.hide-direct-debit | default: false %}
{% assign hide-mobile-pay = include.hide-mobile-pay | default: false %}

The `prices` resource lists the prices related to a specific payment.

{:.code-header}
**Request**

```http
GET /psp/creditcard/payments/5adc265f-f87f-4313-577e-08d3dca1a26c/prices/ HTTP/1.1
Host: api.externalintegration.payex.com
Authorization: Bearer <MerchantToken>
Content-Type: application/json
```

{:.code-header}
**Response**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "payment": "/psp/creditcard/payments/5adc265f-f87f-4313-577e-08d3dca1a26c",
    "prices": {
        "id": "/psp/creditcard/payments/5adc265f-f87f-4313-577e-08d3dca1a26c/prices",
        "priceList": [
            {
                "type": "VISA",
                "amount": 2350,
                "vatAmount": 0
            },
            {
                "type": "MasterCard",
                "amount": 2350,
                "vatAmount": 0
            }
        ]
    }
}
```

{:.table .table-striped}
| Property                       | Type      | Description                                                                                                                                                                                 |
| :----------------------------- | :-------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `payment`                      | `string`  | The relative URI of the  `payment`  the prices resource belongs to.                                                                                                                         |
| `prices.id`                    | `string`  | The relative URI of the current  `prices`  resource.                                                                                                                                        |
| `prices.priceList`             | `array`   | The array of price objects. **Note:** Even if you specifiy  `CreditCard`  in the input message the system will return all your configured card brands instead when you expan the priceList. |
| `prices.priceList[].type`      | `string`  | The type of the price object.                                                                                                                                                               |
| `prices.priceList[].amount`    | `integer` | Amount is entered in the lowest momentary units of the selected currency. E.g. 10000 = 100.00 NOK, 5000 = 50.00 SEK.                                                                        |
| `prices.priceList[].vatAmount` | `integer` | If the amount given includes VAT, this may be displayed for the user in the payment page (redirect only). Set to 0 (zero) if this is not relevant.                                          |

### Prices Object Types

Each payment instrument have one or more prices object types. This is most
relevant when using card based and direct debit payments as each type correspond
to a card brand or bank respectively.

#### Card Payments

The generic type `CreditCard` enables all card brands, supported by merchant
contract.

{:.table .table-striped}
| Type            | Description                                |
| :-------------- | :----------------------------------------- |
| `Visa`          | Visa                                       |
| `MasterCard`    | MasterCard                                 |
| `Amex`          | American Express                           |
| `Dankort`       | Dankort can only be used with DKK currency |
| `Diners`        | Diners Club                                |
| `Finax`         | Finax                                      |
| `Jcb`           | JCB                                        |
| `IkanoFinansDK` | Ikano Finans Denmark                       |
| `Maestro`       | MasterCard Maestro                         |

{% unless hide-direct-debit %}

#### Direct Debit Payments

The generic type `DirectDebit` enables all bank types, supported by merchant
contract.

{:.table .table-striped}
| Type         | Description                                      |
| :----------- | :----------------------------------------------- |
| `SwedbankLV` | Swedbank Latvia                                  |
| `SwedbankEE` | Swedbank Estonia                                 |
| `SwedbankLT` | Swedbank Lithuania                               |
| `SwedbankSE` | Swedbank Sweden **(Not yet supported)**          |
| `AalandFI`   | Ålandsbanken Finland **(Not yet supported)**     |
| `AktiaFI`    | Aktia Finland **(Not yet supported)**            |
| `DDBFI`      | Danske Bank Finland **(Not yet supported)**      |
| `HSBSE`      | Handelsbanken Sweden **(Not yet supported)**     |
| `NordeaFI`   | Nordea Finland **(Not yet supported)**           |
| `NordeaSE`   | Nordea Sweden **(Not yet supported)**            |
| `OmaFI`      | Oma säästöpankki Finland **(Not yet supported)** |
| `OPFI`       | OP Finland **(Not yet supported)**               |
| `POPFI`      | POP Pankki **(Not yet supported)**               |
| `SHBFI`      | Handelsbanken Finland **(Not yet supported)**    |
| `SpankkiFI`  | S-Pankki Finland **(Not yet supported)**         |
| `SPFI`       | Säästöpankki Finland **(Not yet supported)**     |
{% endunless %}

#### Invoice Payments

{:.table .table-striped}
| Type      | Description    |
| :-------- | :------------- |
| `Invoice` | Always Invoice |

{% unless hide-mobile-pay %}

#### MobilePay Payments

{:.table .table-striped}
| Type        | Description      |
| :---------- | :--------------- |
| `Mobilepay` | Always Mobilepay |

{% endunless %}

#### Swish Payments

{:.table .table-striped}
| Type    | Description  |
| :------ | :----------- |
| `Swish` | Always Swish |

#### Vipps Payments

{:.table .table-striped}
| Type    | Description  |
| :------ | :----------- |
| `Vipps` | Always Vipps |