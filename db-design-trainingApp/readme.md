Fitness Influencer Coaching Platform – ER Diagram
 Overview

This project represents the Entity-Relationship (ER) diagram for a Fitness Influencer Coaching Platform.

The platform enables fitness trainers/influencers to:

Onboard clients
Sell fitness plans/programs
Schedule consultations or live sessions
Track client progress
Manage subscriptions and payments
 Objective

Design a scalable and practical database structure that supports:

Trainer-client relationships
Plan subscriptions
Session scheduling
Progress tracking
Payment handling

-- Core Entities --

1. customers
Stores primary information about the platform's customers.

customer_id (SERIAL, PK): Unique identifier for the customer.
customer_first_name (varchar(50), NOT NULL): First name.
customer_last_name (varchar(50), NOT NULL): Last name.
customer_phone_number (varchar(13)): Phone number.
customer_email (varchar(200), NOT NULL): Email address.
customer_password (varchar(100), NOT NULL): Encrypted password.
customer_profile_photo (url): URL to the user's profile photo.
customer_detaile (text): Any additional text details about the customer.

2. trainers
Stores information about the trainers/experts on the platform.

trainer_id (SERIAL, PK): Unique identifier for the trainer.
trainer_phone_number (number, NOT NULL): Phone number.
trainer_first_name (varchar(50), NOT NULL): First name.
trainer_last_name (varchar(50), NOT NULL): Last name.
trainer_email (varchar(200), NOT NULL): Email address.
trainer_password (varchar(100), NOT NULL): Encrypted password.
trainer_ig_handle (varchar(50)): Instagram handle.

3. programs
Defines the different fitness training programs available for enrollment.

program_id (SERIAL, PK): Unique identifier for the program.
program_name (varchar(20)): Short name of the program.
program_description (text): Full description of the program.
program_cost (number): Price of the program.
program_duration (number): Duration of the program in months.

4. enrolements
Tracks which customers are enrolled in which programs.

serial_number (SERIAL, PK): Unique enrollment identifier.
customer_id (number, FK): References customers.
program_id (number, FK): References programs.
enroled_at (date): The date of enrollment.
finish_at (date): The targeted or actual finish date.

5. sessions
Logs the individual training sessions between a trainer and an enrolled customer.

session_id (SERIAL, PK): Unique session identifier.
customer_id (number, FK): References customers.
trainer_id (number, FK): References trainers.
session_date (date, NOT NULL): The scheduled date.
session_start_time (datetime, NOT NULL): The start time.
session_end_time (datetime, NOT NULL): The end time.

6. consultations
Logs consultation meetings scheduled between customers and experts (trainers).

cosultation_id (SERIAL, PK): Unique consultation identifier.
customer_id (number, FK): References customers.
expert_id (number, FK): References trainers.
consultation_date (date, NOT NULL): The scheduled consultation date.
consultation_time (datetime, NOT NULL): The scheduled consultation time.

7. diets
Holds information related to the diet plans assigned to customers by an expert.

diet_id (SERIAL, PK): Unique diet assignment identifier.
customer_id (number, FK): References customers.
expert_id (number, FK): References trainers.
assigned_at (date, NOT NULL): The date the diet was assigned.
diet_plan (text, NOT NULL): The actual content of the diet plan.

8. workout_plans
Stores the workout plans specifically customized and assigned to the clients.

workout_plan_id (SERIAL, PK): Unique workout plan identifier.
customer_id (number, FK): References customers.
expert_id (number, FK): References trainers.
assigned_at (date, NOT NULL): The date the plan was assigned.
workout_plan (text, NOT NULL): The content of the assigned workout plan.

9. customer_details_collected
Maintains records on specific health matrices and special needs per customer.

detail_id (SERIAL, PK): Unique detail record.
customer_id (number, FK): References customers.
collected_by (number, FK): References trainers who recorded this information.
customer_weight (number, NOT NULL): Recorded weight of the customer.
customer_height (number, NOT NULL): Recorded height of the customer.
special_notes (text): Medical conditions or special needs.

10. trainer_transfer_log
For accountability and legal compliance, ensures logging whenever a customer is transferred to a new trainer.

transfer_log_id (SERIAL, PK): Unique log ID.
current_trainer_id (number, FK, NOT NULL): References trainers (the previous trainer).
new_trainer_id (number, FK, NOT NULL): References trainers (the new, assigned trainer).
customer_id (number, FK, NOT NULL): References customers.
transferd_at (date): Date of the trainer transfer.
reason (text): Reason for the transfer.
updated_detail (text): Extra details about the transfer.

11. consistency_table
Metrics table to track and gamify client active participation.

customer_id (number, FK): References customers.
current_streak (number): Active days streak.
last_active_day (date): Last recorded activity time.
longest_streak (number): Overall maximum active streak.

12. payment_history
Tracks transactions related to customer program enrollments.

transaction_id (SERIAL, PK, NOT NULL): Unique transaction reference.
customer_id (number, FK): References customers.
program_id (number, FK): References programs.
date_of_enrolement (date): Timestamp mapping to payment confirmation.

-- Relationships & Cardinality--
A User can be a Trainer or Client (1:1 specialization)
A Trainer can create multiple Plans (1)
A Client can subscribe to multiple Plans (M via Subscription)
A Plan can have multiple Clients
A Subscription can have multiple Payments
A Trainer and Client can have multiple Sessions
A Client can submit multiple Check-ins
A Client can have multiple Progress records
A Trainer can add notes for multiple clients
