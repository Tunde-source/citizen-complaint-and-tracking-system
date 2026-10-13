# citizen-complaint-and-tracking-system
make complaint tracking easier base.
# Citizen Complaint and Tracking System

A simple Python program that lets citizens file complaints with government offices,
get a **reference number**, and track what happened. Authorized officers can
**assign, investigate and resolve** each complaint.

## Task 1 - OOP Basics
The program has four classes relevant to the domain:

| Class | Purpose |
|---|---|
| `Citizen` | A person who files and tracks complaints |
| `Officer` | An authorized government staff member (Supervisor or Investigator) |
| `Government Department` | A ministry, agency or council that receives complaints and has officers |
| `Complaint` | One complaint: reference number, status, assigned officer, history |

## Privacy: no sensitive personal data
The system stores **only**: a citizen ID (e.g. `C1`), a name (a nickname is fine),
and the complaint title/description. It does **not** store national ID numbers, phone
numbers, emails, addresses, passwords or financial data. Nothing is saved to a file or
database; all data is kept in memory and is erased when the program closes. The program
also reminds citizens not to type personal details into their complaint. All sample
names are made up.

## How to run
Requires Python 3 only (no extra libraries).

```
python complaint_basic.py
```
Then use the numbered menu. If you use an online compiler, type your menu answers in
its "input" box, one per line.

## Sample logins (built in)
| ID | Who |
|---|---|
| `C1`, `C2` | Citizens (John, Mary) |
| `O1` | Amina - Water supervisor |
| `O2` | Daniel - Water investigator |
| `O3` | Grace - Roads supervisor |

Department codes: `WATER`, `ROADS`.

## Example walkthrough
1. Menu 1: citizen `C1` files a complaint to `WATER` and receives `CMP-0001`.
2. Menu 4: officer `O1` (supervisor) chooses **b** and assigns `CMP-0001` to `O2`.
3. Officer `O2` chooses **c** (start investigation), then **d** (resolve with a note).
4. Menu 2: citizen `C1` tracks `CMP-0001` and sees the full history.
5. Menu 3: citizen `C1` closes the resolved complaint.

## Rules enforced
- Every complaint gets a unique reference number (`CMP-0001`, `CMP-0002`, ...).
- Only a **supervisor** can assign a complaint, and only within their own department.
- Only the **assigned officer** can start investigation or resolve.
- Only a supervisor or the assigned officer can reject.
- Only the **citizen who filed** a complaint can track or close it.
- Status order: Submitted -> Assigned -> Under Investigation -> Resolved -> Closed
  (or Rejected). Steps cannot be skipped.

## Limitations
- No passwords: anyone who types an ID can act as that person (fine for a class demo).
- Data is not saved between runs.
- Citizens choose the department themselves.
