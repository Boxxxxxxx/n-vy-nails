# N-Vy Nails

## Architecture

N-Vy Nails will have 2 domains.

### www.nvynails.com

**Responsibilities:**

- Marketing pages
- Client portal
    - Gallery
    - Google Business Reviews API

### employee.nvynails.com

**Responsibilities:**

- BIS | Business Information Systems
    - Inventory
    - Employee Availability
- CRM | Customer Relationship Manager
    - Clients
        - Client Reward Points
    - Bookings
- CMS | Content Management System
    - Gallery
    - Events
- AuthZ/N - RBAC
    - Admins
        - Privileges
            - CRUD on BIS/\*
            - CRUD on CRM/\*
            - CRUD on CMS/\*
        - Interactions
            - Dashboard View
                - In-person traffic / Busy hours
                - Inventory
                - P&L
                - Bookings
                - Hosts
                - Employees
            - Client Management
                - Create a client
                - Read all clients
                - Update a client (and reward points)
                - Delete a client
            - Employee Availability Management
                - Create a timeslot
                - Read all timeslots
                - Update a timeslot
                - Delete a timeslot
            - Booking Management
                - Create a booking
                - Read all bookings
                - Update a booking
                - Delete a booking
            - Inventory Management
                - Create a product
                - Read all products
                - Update a product
                - Delete a product
                - Consider `product_type` junction
            - Gallery Management
                - Create a record
                - Read all records
                - Update a record
                - Delete a record
            - Events Management
                - Create an event
                - Read all events
                - Update an event
                - Delete an event
    - Hosts
        - Privileges
            - CR(U) on the CRM/Clients
                - (U) if updating client reward points, soft update
                    - Send an approval request to Admin
            - CRUD on the CRM/Bookings
            - R on BIS/Employee_Availability
        - Interactions
            - Client Management
                - Create a client
                - Read all clients
                - Update a client's info
                    - Update client reward points (pending admin approval) for comps
            - Booking Management
                - Create a booking
                - Read all bookings
                - Update a booking
                - Delete a booking
            - Employee Availability Management
                - Read all timeslots
    - Employee
        - Privileges
            - R on the CRM/Clients
            - CR(U)(D) on the CRM/Bookings
                - CR Only for themselves
                - (U)(D) Soft update/delete their own bookings
                    - Send an approval request to Admin
            - (C)R(U)(D) on BIS/Employee_Availability
                - (C,U,D) Soft on their own availability, send approval request to Admin
                - Read only their own availability
        - Interactions
            - Booking Management
                - Create a booking for themselves
                - Read their own bookings
                - Soft update their own bookings
                - Soft delete their own bookings
            - Employee Availability Management
                - Soft create their own availability
                - Read their own availability
                - Soft update their own availability
                - Soft delete their own availability
    - Marketer
        - Privileges
            - CRUD on the CMS/\*
        - Interactions
            - Gallery Management
                - Create a record
                - Read all records
                - Update a record
                - Delete a record
            - Events Management
                - Create an event
                - Read all events
                - Update an event
                - Delete an event

## Monorepo Architecture

### Monorepo Tooling

- [Turborepo](https://turborepo.com/docs)

### Monorepo Package Management

- PNPM (v10, feel free to upgrade/downgrade)`
