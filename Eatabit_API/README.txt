### Introduction
---
This site documents the Eatabit API endpoints. The current version is **v8**.
</br>
</br>

### Authentication
---

All API requests require authentication using HTTP Basic. You can find your API credentials by logging into the API dashboard at [https://api.eatabit.io](https://api.eatabit.io).

There are two sets of authentication credentials: **development** and **production**. The only difference between the two account types is that Jobs sent to the API with **development** credentials will not be sent to the printer. This may be useful for development when you do not yet have a physical printer.

Use your API **SID** and **TOKEN** as **username** and **password** for HTTP Basic.
</br>
</br>

### Status callbacks
---

Job Status Callbacks allow you to passively monitor the State of your Jobs. When your Job changes State, for example, from “downloaded” to “printed”, a Job Status Callback will fire to the url that you specified in the **status_url** value of the Job, using the HTTP method specified in the **status_url_method** value, with the GET Job schema for the API version you used to create the Job.

The following table shows support for Job States on different Printer models

| State | Description | v5 | v6 | v7 | v8 |
| --- | --- | --- | --- | --- | --- |
|queued|The Job has been received by Eatabit|✓|✓|✓|✓|
|downloaded| The Job has been downloaded to the Printer|✓|✓|✓|✓|
|printed|The Job has been printed by the Printer|✓|✓|✓|✓|
|accepted|The Printer user has marked the Job as Accepted||||✓|
|rejected|The Printer user has marked the Job as Rejected||||✓|

<br/>

### Ticket formatting
---

Jobs can optionally be formatted to enhance readability and accuracy.

* **Newlines**
  * `\n`
* **Emphasis**
  * `<b>bold</b>`
  * `<lg>large font</lg>`
  * `<u>underlined</u>`
* **Alignment**
  * `<center>centered</center>`
  * `<right>right-aligned</right>`

> Jobs are printed left-aligned by default. Use these tags to temporarily change alignment.

> Changing alignment will cause the thermal printer to feed to the next line. So it is not possible to print left and right aligned text on the same line.

> Printers only accept ASCII characters. A `?` character will be substituted for any non-ASCII characters present in the Job body.

**Barcodes**
The following barcode types are supported: [UPC-A](https://en.wikipedia.org/wiki/Universal_Product_Code), [EAN13 and EAN8](https://en.wikipedia.org/wiki/International_Article_Number), [Code 39](https://en.wikipedia.org/wiki/Code_39), [ITF](https://en.wikipedia.org/wiki/Interleaved_2_of_5), [Codabar](https://en.wikipedia.org/wiki/Codabar), [Code 93](https://en.wikipedia.org/wiki/Code_93), and [Code 128](https://en.wikipedia.org/wiki/Code_128).

| Tag | Permitted Characters | Size |
| --- | --- | --- |
| `<upc_a>` | 0-9 | 11 or 12 chars |
| `<ean13>` | 0-9 | 12 or 13 chars |
| `<ean8>` | 0-9 | 7 or 8 chars |
| `<code39>` | 0-9, A-Z, space, %, +, -, ., /, $ | 1-255 chars |
| `<itf>` | 0-9 | 2-254 chars, even number |
| `<codabar>` | 0-9, A-D, $, +, -, ., /, : | 1-255 chars |
| `<code93>` | valid Base64 string | 1-255 decoded bytes |
| `<code128>` | valid Base64 string | 2-255 decoded bytes |

**Barcode examples**
* `<upc_a>01234567890</upc_a>`
* `<code93>KmM=</code93>` (barcode encoding "\x2A\x63")

Note that Code 93 and Code 128 barcode information has to be given in Base64, since it is possible to encode binary data.