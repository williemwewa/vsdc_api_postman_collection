# ZRA VSDC API Integration

This repository contains a Postman collection for integrating with the Zambia Revenue Authority's Virtual Sales Data Controller (VSDC) API. The collection provides a comprehensive set of endpoints and examples for connecting third-party systems with the ZRA Smart Invoice platform.

## Overview

The VSDC API enables businesses to seamlessly integrate their Enterprise Resource Planning (ERP) systems or Certified Invoicing Systems (CIS) with ZRA's Smart Invoice system. This integration allows for:

- Electronic invoicing processes
- Stock management and tracking
- Sales and purchase transactions
- Import operations
- Tax compliance

## Requirements

- Postman (latest version recommended)
- VSDC API deployed in your environment
- API access credentials (TPIN, Branch ID, and Device Serial Number provided by ZRA)
- Valid ZRA Smart Invoice registration

## Installation

1. Clone this repository to your local machine.
2. Import the Postman collection:
   - Open Postman
   - Click on the "Import" button
   - Select the `ZRA_VSDC_API_Collection.json` file from this repository
3. Set up your environment variables:
   - Create a new environment in Postman
   - Add a variable named `base_url` with the value of your VSDC API endpoint (e.g., `http://localhost:8080/zravsdc`)

## Getting Started

### Device Initialization

The first step in using the VSDC API is to initialize your device. This is a one-time process that retrieves security keys and configuration settings:

1. Navigate to the "Device Initialization" folder in the collection
2. Open the "Device Initialization" request
3. Update the request body with your TPIN, Branch ID, and Device Serial Number
4. Send the request
5. Store the returned information securely for future reference

### Core Workflows

The collection is organized into several key areas:

1. **Standard and Classification Codes** - Retrieve reference data needed for other API calls
2. **Branch Information** - Manage branch details and users
3. **Customer Information** - Manage customer records
4. **Item Information** - Register and manage products/services
5. **Import Information** - Process imported items
6. **Sales Information** - Record various types of sales transactions
7. **Purchase Information** - Record and retrieve purchase data
8. **Stock Information** - Manage inventory levels

## API Endpoints Reference

### 1. Device Initialization
- `POST /initializer/selectInitInfo` - Initialize the device and retrieve API keys

### 2. Standard and Classification Codes
- `POST /code/selectCodes` - Get standard codes
- `POST /itemClass/selectItemsClass` - Get classification codes
- `POST /notices/selectNotices` - Get system notices

### 3. Branch Information
- `POST /branches/selectBranches` - Get all branches
- `POST /branches/saveBrancheUser` - Register branch users
- `POST /branches/saveBrancheCustomers` - Register branch customers

### 4. Customer Information
- `POST /customers/selectCustomer` - Retrieve customer details

### 5. Item Information
- `POST /items/saveItem` - Register new items
- `POST /items/updateItem` - Update existing items
- `POST /items/selectItems` - Get all items
- `POST /items/selectItem` - Get specific item details
- `POST /items/saveItemComposition` - Manage composite items
- `POST /items/saveRrpItems` - Save recommended retail prices
- `POST /items/selectRrpItems` - Get recommended retail prices

### 6. Import Information
- `POST /imports/selectImportItems` - Get imported items
- `POST /imports/updateImportItems` - Update import status

### 7. Sales Information
- `POST /trnsSales/saveSales` - Record sales transactions (supports multiple types)
- `POST /trnsSales/selectPrincipals` - Get RVAT principals
- `POST /trnsSales/selectInvoice` - Retrieve invoice details

### 8. Purchase Information
- `POST /trnsPurchase/selectTrnsPurchaseSales` - Get purchases
- `POST /trnsPurchase/savePurchase` - Record purchase transactions

### 9. Stock Information
- `POST /stock/selectStockItems` - Get stock items
- `POST /stock/saveStockItems` - Record stock movements
- `POST /stockMaster/saveStockMaster` - Update stock quantities

## Transaction Flow Examples

### Recording a Sale
1. Fetch standard and classification codes
2. Create/verify item records
3. Execute `saveSales` endpoint with appropriate transaction details
4. Update stock using `saveStockItems`
5. Update total inventory with `saveStockMaster`

### Processing Imports
1. Retrieve imports using `selectImportItems`
2. Acknowledge imports with `updateImportItems`
3. Update stock using `saveStockItems`
4. Update total inventory with `saveStockMaster`

## Tax Categories

The collection supports various tax categories:

- VAT Standard Rate (A) - 16%
- Minimum Taxable Value (B) - MTV goods
- Exports (C1) - 0%
- Zero-rating LPO (C2) - 0%
- Zero-rated by nature (C3) - 0%
- Exempt (D) - No tax
- Reverse VAT (RVAT) - For imported services
- Insurance Premium Levy (IPL1, IPL2)
- Tourism Levy (TL)
- Service Charge (F) - 10%

## Notes

- All API responses should be carefully handled and stored for reference
- The Device Initialization endpoint should only be called once
- Always follow the required sequence for dependent operations
- Ensure accurate tax categories are used for all transactions
- After recording purchases, imports, or sales, always update stock records

## Contributing

Contributions to improve this collection are welcome. Please follow these steps:

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a new Pull Request

## License



## Acknowledgements

This collection was created based on the official ZRA VSDC API Specification Document (v1.0.7-1).