# citizen-complaint-and-tracking-system
make complaint tracking easier
# Citizen Complaint and Tracking System

A Python, object-oriented system that lets citizens file complaints with government
bodies, receive a unique **reference number**, and track progress, while authorized
officers **assign, investigate and resolve** each complaint.

## Features

- Unique reference numbers (e.g. `CMP-2026-000001`) for every complaint
- Role-based authorization: **Supervisors** assign cases; **Investigators** work them
- Enforced life cycle: `Submitted → Assigned → Under Investigation → Resolved → Closed`
  (plus `Rejected`, and citizen **reopen** of a resolved case)
- Full audit trail: every status change records who, when and why
- Privacy: only the citizen who filed a complaint can track it
- Department isolation: officers can only act on their own department's complaints
- JSON persistence, an interactive CLI, a scripted demo, and unit tests
- No third-party dependencies (Python 3.9+)

## Project structure

```
complaint_system.py   # everything in one file: models, service layer, demo/CLI, unit tests
README.md
REPORT.md             # design and analysis report
```

## Running

```bash
python complaint_system.py demo   # scripted walkthrough of the full workflow
python complaint_system.py cli    # interactive menu (data saved to data.json on exit)
python complaint_system.py test   # run the 11 unit tests
```

Sample IDs loaded in the CLI: citizens `CIT-0001`, `CIT-0002`; officers `OFF-0001`
(Water supervisor), `OFF-0002` (Water investigator), `OFF-0003` (Roads supervisor).
Departments: `WATER`, `ROADS`.

## Classes

| Class | Responsibility |
|---|---|
| `Citizen` | Registered member of the public; keeps references of their complaints |
| `Officer` | Government employee with a department and a role (Supervisor / Investigator) |
| `GovernmentDepartment` | Receives complaints, holds officers, reports workload |
| `Complaint` | Reference number, status, assignee, resolution, audit history; enforces transitions and permissions |
| `ComplaintSystem` | Facade: registers entities, generates references, persists data |

## Example

```python
# (inside complaint_system.py, or: from complaint_system import Complaint System, Role)

s = Complaint System()
add_department("WATER", "Ministry of Water Resources")
sup = add officer("WATER", "Amina", Role. SUPERVISOR)
inv = .add officer("WATER", "Daniel")
cit = register citizen("John Banda", "NID-1001")

c = submit complaint(cit.citizen_id, "WATER", "No water", "None for 5 days")
s.assign(c.reference, sup.officer_id, inv.officer_id)
s.start_investigation(c.reference, inv.officer_id)
s.resolve(c.reference, inv.officer_id, "Pipe repaired")
print(s.track(c.reference, cit.citizen_id).status)   # Status.RESOLVED
```

## Notes and limitations

- Officer "login" in the CLI is by ID only (no passwords); a real deployment needs authentication.
- Storage is a single JSON file; a production system would use a database.
- The brief lists an `Office` class; this project models the authorized staff as `Officer`
  (and the organisational unit as `GovernmentDepartment`).
