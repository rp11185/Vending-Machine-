# Vending Machine Controller (Verilog)

## Overview
This project implements a **Vending Machine Controller using Verilog HDL**.  
The system is designed using a **Finite State Machine (FSM)** to control product selection, money insertion, payment verification, product dispensing, and change return.

The design currently operates using a **50 MHz system clock**, while the hardware design supports operation up to **300 MHz maximum clock frequency**.

---

## Features
- FSM-based vending machine controller
- Product selection using `product_id`
- Money insertion and validation
- Automatic product dispensing
- Change calculation and return
- Overflow protection for monetary registers
- Timeout logic for abandoned transactions
- Transaction completion signal

---

## System States

The vending machine operates in the following stages:

1. **IDLE** – Waiting for user interaction  
2. **SELECTION** – User selects product  
3. **COLLECTION** – Machine accepts money  
4. **VERIFICATION** – Checks if inserted money is sufficient  
5. **DISPENSE** – Product is delivered  
6. **CLEAR** – Transaction completed and system resets  

---

## Clock Information

- **Current Operating Clock:** 50 MHz  
- **Maximum Supported Clock:** 300 MHz  

The internal timer and timeout logic are designed assuming a **50 MHz clock** for accurate real-time timing.

---

## Inputs

| Signal | Width | Description |
|------|------|-------------|
| `clk` | 1 | System clock (50 MHz) |
| `rst` | 1 | Global reset |
| `selection` | 1 | Product selection signal |
| `dispence` | 1 | Dispense confirmation |
| `cancel` | 1 | Cancel transaction |
| `money_valid` | 1 | Money insertion event |
| `money_value` | 7 | Inserted coin/bill value |
| `product_id` | 4 | Selected product ID |

---

## Outputs

| Signal | Width | Description |
|------|------|-------------|
| `ready` | 1 | Indicates sufficient money inserted |
| `dispenced` | 1 | Transaction completed |
| `product_delivered` | 1 | Product successfully delivered |
| `entered_money` | 9 | Total inserted money |
| `extra_money` | 7 | Overflow money storage |
| `total` | 9 | Total product cost |
| `change_out` | 9 | Returned change |

---

## Timeout Mechanism

To prevent the vending machine from remaining stuck in incomplete transactions:

- A **1-second timer** is generated using a counter
- An **idle counter** tracks inactivity
- If inactivity reaches **120 seconds**, the transaction is automatically cancelled
- Inserted money is returned to the user

---

## Product Quantity Encoding

The quantity of the product is encoded in the **least significant bit of `product_id`**.

| product_id[0] | Quantity |
|---------------|----------|
| 0 | 1 unit |
| 1 | 2 units |

This method reduces hardware complexity while supporting multi-quantity purchases.

---

## Applications

- FPGA based digital design projects  
- Automated vending machine systems  
- FSM based hardware control designs  
- Digital transaction system simulations  

---

## Author

**Ravi Patel**
