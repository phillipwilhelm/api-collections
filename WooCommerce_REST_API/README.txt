Taken from: https://github.com/woocommerce/woocommerce-rest-api-docs

# Introduction

WooCommerce (WC) 2.6+ is fully integrated with the WordPress [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer) API. This allows WC data to be created, read, updated, and deleted using requests in JSON format and using WordPress REST API Authentication methods and standard HTTP verbs which are understood by most HTTP clients.

The current WP REST API integration version is `v3` which takes a first-order position in endpoints. 

The following table shows API versions present in each major version of WooCommerce:

<table><thead>
<tr>
<th>API Version</th>
<th>WC Version</th>
<th>WP Version</th>
<th>Documentation</th>
</tr>
</thead><tbody>
<tr>
<td>`v3`</td>
<td>3.5.x or later</td>
<td>4.4 or later</td>
<td>-</td>
</tr>
<tr>
<td>`v2`</td>
<td>3.0.x or later</td>
<td>4.4 or later</td>
<td>[v2 docs](https://woocommerce.github.io/woocommerce-rest-api-docs/wp-api-v2.html)</td>
</tr>
<tr>
<td>`v1`</td>
<td>2.6.x or later</td>
<td>4.4 or later</td>
<td>[v1 docs](https://woocommerce.github.io/woocommerce-rest-api-docs/wp-api-v1.html)</td>
</tr>
</tbody></table>

Prior to 2.6, WooCommerce has had a REST API separate from WordPress which is now known as the legacy API. You can find the documentation for the legacy API separately.

<table><thead>
<tr>
<th>API Version</th>
<th>WC Version</th>
<th>WP Version</th>
<th>Documentation</th>
</tr>
</thead><tbody>
<tr>
<td>`Legacy v3`</td>
<td>2.4.x or later</td>
<td>4.1 or later</td>
<td>[Legacy v3 docs](https://woocommerce.github.io/woocommerce-rest-api-docs/v3.html)</td>
</tr>
<tr>
<td>`Legacy v2`</td>
<td>2.2.x or later</td>
<td>4.1 or later</td>
<td>[Legacy v2 docs](https://woocommerce.github.io/woocommerce-rest-api-docs/v2.html)</td>
</tr>
<tr>
<td>`Legacy v1`</td>
<td>2.1.x or later</td>
<td>4.1 or later</td>
<td>[Legacy v1 docs](https://woocommerce.github.io/woocommerce-rest-api-docs/v1.html)</td>
</tr>
</tbody></table>

## Requirements

To use the latest version of the REST API you must be using:

*   WooCommerce 3.5+.
*   WordPress 4.4+.
*   Pretty permalinks in `Settings > Permalinks` so that the custom endpoints are supported. **Default permalinks will not work.**
*   You may access the API over either HTTP or HTTPS, but *HTTPS is recommended where possible*.

If you use ModSecurity and see `501 Method Not Implemented` errors, see [this issue](https://github.com/woocommerce/woocommerce/issues/9838) for details.
