---
description: Mapping of fields to the OMS Entities -
---

# Mapping

|                        |           |                                                                     |                                                                                                                                                                           |
| ---------------------- | --------- | ------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Fields**             | **Type**  | **Description**                                                     | **HC Entity Mapping**                                                                                                                                                     |
| externalId             | string    | This is the external ID assigned to an order.                       | Shipment.externalId                                                                                                                                                       |
| shipmentItemExternalId | string    | This is the external ID assigned to an Order Item.                  | shipmentItem.externalId                                                                                                                                                   |
| quantity               | number    | This is the quantity of an order Item                               | shipmentItem.quantity                                                                                                                                                     |
| statusId               | string    | This is the status ID of the Shipment                               | Shipment.statusId                                                                                                                                                         |
| shipmentTypeId         | string    | This is the type ID of the Shipment                                 | Shipment.shipmentTypeId                                                                                                                                                   |
| shipmentId             | string    | This is a unique ID assigned to the shipment.                       | ShipmentReceipt.shipmentId                                                                                                                                                |
| shipmentItemSeqId      | string    | This is the Seq ID assigned to the shipment Item                    | ShipmentReceipt.shipmentItemSeqId                                                                                                                                         |
| receiptId              | string    | This is the unique ID assigned to the receipt of the shipment Item. | ShipmentReceipt.receiptId                                                                                                                                                 |
|                        |           |                                                                     |                                                                                                                                                                           |
| receivedDate           | date-time | This is the date when the shipment receipt received                 | ShipmentReceipt.datetimeReceived                                                                                                                                          |
| totalQuantityAccepted  | number    | This is the total quantity accepted of the shipment receipt         | ShipmentReceipt.quantityAccepted                                                                                                                                          |
| totalQuantityRejected  | number    | This is the total quantity rejected of the shipment receipt         | ShipmentReceipt.quantityRejected                                                                                                                                          |
| totalReceivedQuantity  | number    | This is the total received quantity of the shipment receipt         | <p>ShipmentReceipt.quantityAccepted<br><br><strong>NOTE:</strong> The <strong>totalReceivedQuantity</strong> is the sum of the quantityAccepted of the shipment item.</p> |

