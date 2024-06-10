---
description: >-
  Learn about the order approval process at ADOC, including address validation
  and the requirement for a government-mandated Customer ID, with a focus on
  importing order metafields from Shopify to HC.
---

# Order Approval

ADOC uses a custom flow where certain orders are only approved after the address is validated and a government-mandated Customer ID is present. After an order is imported, ADOC has a job enabled for importing order metafields, under the namespace “HotwaxOrderDetails”, from Shopify by an independent job as Order Attributes in HotWax Commerce.

## Sync metafields from Shopify

To synchronize order meta fields from Shopify, we have configured a workflow that utilizes NiFi custom flows and Moqui Services. 
The process can be divided into four main steps:

1. **Preparing File for Shopify API Request**:
   NiFi fetches all orders from the database that lack the required meta fields: `customerId` and `municipio`. The dataset with missing meta fields is converted into a JSON file suitable for a Shopify API request.


2. **Shopify API Call**:
   NiFi calls the Shopify API to obtain the current meta fields under the namespace "HotwaxOrderDetails". The response from Shopify is received in JSON format.


3. **Transformation of API Response**:
   The JSON response from Shopify is not directly understandable by the OMS. NiFi processes this JSON file to convert it into a format that OMS can accept.


4. **Job Picking and Data Import**:
   The transformed file is placed in an FTP location for OMS. A job in the Job Manager's Packaged Multi-Stream Import, under the Miscellaneous section, picks up the file and imports the data into OMS.

This workflow ensures efficient synchronization of order meta fields from Shopify to OMS, maintaining data accuracy and consistency.

#### To ensure the job runs properly, we need to verify the following:
1. The corresponding custom NiFi flow is running properly.
2. The Moqui service job poll_OMSOrderIdsFeed_ADOC is scheduled.

If the metafield sync is running as expected, on the order detail page these attributes should be present:

1. Customer ID
2. Municipio
3. SHIPTO\_ADDRESS\_UPDATED: true

The `SHIPTO_ADDRESS_UPDATED` order attribute is created after an order has been first validated for a registered Municipio order attribute value. If this attribute is not created, that means that the order does not have a valid Municipio attribute and one needs to be added.

Validate that the Order Item Attribute job for this is enabled.

Validate that the config ID is set correctly. The default config ID is: `IMP_ORDER_ITM_ATTR`

You can use the “Missing Order Attribute” report to identify orders where the OMS could not automatically correct the address of an order.

## Metafields created on Shopify but not imported into HotWax

Go to the Shopify order details page > add /metafields.json in the URL> verify the order creation and metafields input time.

If you cannot wait for metafields to be imported or the job is not working as expected, order attributes can be created manually from the Order Detail page.

Mapping Central American region types to the OMS's North American Region types helps when troubleshooting order approval flows in the OMS. If the address entered into the order is not mapped correctly to the type of region, then the order will not be approved even if the region name exists.

| Central American Region | North American Region Type |
| ----------------------- | -------------------------- |
| Departamento            | State                      |
| Municipio               | Municipality               |
| Canton                  | Canton                     |
| Distrito                | District                   |

Read [the Glossary](../GLOSSARY.md) to learn more about how the Central American Regions maps to the Carrier Geo Mapping entries in the OMS.
