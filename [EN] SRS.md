

# [EN] SRS - Study Cafe Kiosk Software Requirements Specifications

This is an SRS for a study cafe kiosk.

## 1. Introduction

### 1.1 Purpose

This software allows study cafe users to log in with phone numbers, purchase passes, and select seats using kiosks.

### 1.2 Scope

- This software is for kiosk usage ONLY, and operates separately from the mobile system.
- This software operates separately from normal product sales functions.

### 1.3 Definitions

- One-day pass: This pass allows the user to access the study cafe for 12 hours on the same day it was purchased.
- Time pass: This pass allows the user to access the study cafe for a set amount of time, starting from the day it was purchased. The time is deducted from the amount based on entrance and exit records. (ex. 40-hour pass, 100-hour pass)
- Period pass: This pass allows the user to access the study cafe for a set period, starting from the day it was purchased. (ex.  week pass, month pass, 3-month pass)
- Occupy seat: This refers to the act of selecting a seat to use for the day through the software before entering the study cafe. The occupied seat is valid until the user exits or until the pass expires.

## 2. Overall Description

### 2.1 Product Summary

This software allows users to:

- use their phone numbers to log in
- select the pass
- pay&purchase the pass
- look at the seating chart
- occupy seats
- enter&exit the study cafe

### 2.2 Users

- Study cafe user: requires simple UI for easy and fast access
- Study cafe manager: Little to no IT experience, requires simple UI for monitoring real-time usage and managing pass sales.

### 2.3 Constraints

- This software will run only on kiosks equipped with payment modules.
- This software will need to be connected to hardware that can automatically open doors and turn on lights to operate.

## 3. Functional Requirements

The software should:

1. provide functions that allow users to log in using their mobile phone number. 
2. provide a screen that displays the passes and allows the users to select a pass and pay with a connected payment module.
3. display the real-time seating arrangement visually on the screen.
4. give priority to the user who first chose the seat for 5 minutes and restrict access from other users, if the same seat was selected at the same time on two or more kiosks.
5. deduct the leftover time by rounding up to 10-minute increments based on the enterance/exit timestamp for time pass users.
6. allow period pass users to select and reserve their seat for long-term use during their use period.
7. require the user to log in with their mobile phone number when entering and exiting the study cafe.

## 4. Non-Functional Requirements

- Performance: the software should take less than 1.5 seconds to respond to on-screen activities such as seat selection or payment requests.
- Availability: the software should work as intended 24/7 without server failure.
- Security: the software should encrypt the data with the AES-256 system to protect personal information such as mobile phone numbers and payment data.
- Stability: the software should allow the door to open even in the case in which it loses network for less than 30 seconds.

## 5. External Interface Requirements

- User Interface
    - Main/login: keypad for mobile phone number input, buttons for [entrance], [exit], and [purchase pass]
    - Product: a list of available one-day, time, and period passes, and their respective prices
    - Seating chart: display of the seating layout modeled after the cafe, with availability for each seat
    - Payment: display with instructions for different payment methods, progress bar
- Hardware Requirements
    - Kiosk: receipt printer, IC/MS card reader, barcode/QR scanner
    - Enterance/exit system: automatic door control board (relay controller) to receive signals from the kiosk to open/close doors
    - Seating Control: IoT controller to power and turn on lights for seats when entering
- Software Interface
    - Payment API: third-party PG payment terminal module (linked with Windows DLL or Local Web storage)
    - Database: real-time seating chart table, user access log table

## 6. Assumptions and Dependencies

- Assumptions
    - The cafe is always connected to a stable broadband internet (WI-FI or cable connection).
    - The user has a mobile phone number that is registered to them or is able to receive calls and messages.
    - The manager has basic knowledge to set up and maintain this software.
- Dependencies
    - The payment function of this software relies on the third-party PG service and its fully functional module authorization and servers.
    - The software relies on the API/protocol standards provided by the hardware manufacturer for automatic doors and light control.

## 7. System Architecture Diagram

<img width="603" height="373" alt="SRS_diagram" src="https://github.com/user-attachments/assets/d2fc2def-cb2c-4cb2-9578-319b587cc74c" />
