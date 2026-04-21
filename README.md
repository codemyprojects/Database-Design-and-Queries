# Database-Design-and-Queries

ER Diagram Description – NTILU Database

The ER diagram represents a Membership Management System designed to handle users, member records, geographic hierarchy, and financial transactions. The database is structured into four main schemas: Administration, dbo, Setup, and Membership, each serving a specific functional purpose.

1. Administration Schema

This schema manages system authentication and login functionality.

LoginUser
Stores user credentials such as username and password.
Includes fields for account status (IsActive) and audit tracking (CreatedBy, CreatedDate).

2. dbo Schema (Core User Management)

This schema defines system users and roles.

Role
Defines different user roles (e.g., Admin, Staff).
UserDistrict / UserDistrict1
Stores detailed user information:
Personal details (name, email, phone)
Organizational assignment (district, post)
Role and permissions
Includes status flags like IsActive, IsEmployee, UserCentral.

Relationships:

A Role can be assigned to many users.
A District and Post are linked to users.


3. Setup Schema (Master / Reference Data)

This schema contains lookup tables used across the system to ensure data consistency.

Zone → District → VDC → Unit
Represents hierarchical geographic structure.
Post
Defines job or organizational positions.
Education
Stores education levels.
License
Stores licensing information.
MemberType
Defines types of membership.

Relationships:

One Zone has many Districts
One District has many VDCs
One VDC has many Units

4. Membership Schema (Core Business Logic)

This schema handles member records and transactions.

Membership
Central entity storing member details:
Personal info (name, contact)
Location (District, Zone, VDC)
Attributes (Education, License, MemberType)

Relationships:

Linked to multiple Setup tables
Parent table for renewals and vouchers
RenewMembership
Tracks membership renewal history:
Renewal number
Renewal date
Expiry date
Payment amount

Relationship:

One Membership → Many RenewMembership
Voucher
Records financial transactions:
Payment details
Voucher number
Payment mode

Relationships:

Linked to Membership
Optionally linked to RenewMembership
🔗 5. Key Relationships Summary
Role → UserDistrict (1-to-Many)
Zone → District → VDC → Unit (Hierarchical)
Membership → RenewMembership (1-to-Many)
Membership → Voucher (1-to-Many)
RenewMembership → Voucher (Optional relationship)

6. Overall System Purpose

This database is designed to:

Manage user authentication and roles
Maintain member records and profiles
Track membership lifecycle (registration & renewal)
Store geographic and organizational hierarchy
Record financial transactions (vouchers)
Ensure data consistency via master tables
Provide audit tracking for all records
