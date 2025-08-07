# 📦 StockShifter-SAP-ABAP

A custom **SAP ABAP** program that enables users to simulate and process **Goods Issue** and **Stock Transfer** using the standard SAP function module `BAPI_GOODSMVT_CREATE`.

This tool allows seamless handling of inventory updates for scenarios such as consumption (movement type 201) and stock transfer (movement type 311), based on user-defined parameters from a custom selection screen built with the **Screen Painter**.

---

## 🔍 Project Overview

**InventoryFlow-BAPI** is designed to:
- Automate goods movement operations (issue and transfer)
- Update inventory records using standard SAP BAPI
- Allow users to select the type of movement via a simple UI
- Commit or rollback based on BAPI response
- Display messages from the BAPI return table for better user feedback

---

## 🧠 Core Functionality

| Operation        | BAPI GM Code | Movement Type | Description                  |
|------------------|--------------|----------------|------------------------------|
| **Stock Transfer** | `04`         | `311`         | Transfers stock from one storage location to another |
| **Goods Issue**   | `03`         | `201`         | Issues stock for consumption (e.g. production/sales) |

---

## 🛠️ Technologies & SAP Concepts

- **ABAP Report Programming**
- **BAPI_GOODSMVT_CREATE**
- **Module Pool Selection Screens (Screen Painter)**
- **Conditional screen logic using SCREEN-GROUP1**
- **BAPI Return Handling (`BAPIRET2`)**
- **Transaction Commit & Rollback**

---

## 📋 Program Structure

### 🔘 Selection Screen (via Screen Painter)

- **Radio Buttons**: Choose between:
  - `Transfer` (stock transfer)
  - `Consume` (goods issue)

- **Dynamic Input Blocks**:
  - When "Transfer" is selected → only transfer-specific fields are active
  - When "Consume" is selected → only issue-specific fields are shown

<img width="1365" height="716" alt="image" src="https://github.com/user-attachments/assets/efc16767-c951-4147-a1ad-78950640d0a8" />

---

### 🔄 Business Logic

#### 📦 Transfer Flow (`PERFORM TRANSFER`)

- Sets movement type to `311`
- Populates required fields like Material, Plant, Storage Location, Quantity
- Executes `BAPI_GOODSMVT_CREATE`
- On success: `BAPI_TRANSACTION_COMMIT`
- On failure: `BAPI_TRANSACTION_ROLLBACK`
- Displays detailed return messages



#### 🔧 Goods Issue Flow (`PERFORM CONSUME`)

- Sets movement type to `201`
- Populates consumption-related details
- Executes `BAPI_GOODSMVT_CREATE`
- Uses standard commit/rollback logic
- Return messages printed for transparency

  📈 Future Enhancements
Add support for other movement types (e.g., 261, 101)

Add dropdowns or search helps (F4) for material/plant fields

Provide report log via spool or email

Add ALV-based output for document summary

👨‍💻 Author
Trupti Kumkar
SAP ABAP Developer Intern VECV
