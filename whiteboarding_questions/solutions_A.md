## Question One: Employees Query

You are given a PostgreSQL database with two tables: the first is an `employees`
table and the second is a `departments` table. Employees can belong to a single
department.

1.  Write a SQL query that, given a department name, finds all the employees
    `name`s that are in that department.

2.  Next find the name of the employees that don't belong to any department

SELECT
    employees.name
FROM
    employees
        join
    departments on departments.id = employees.department_id
WHERE
    departments.name = given_name;

SELECT
    employees.name
FROM
    employees
WHERE
    employees.id IS NULL

## Question Two:

Describe the differences between a primary key and a foreign key.

A primary key is unique id of a table, whereas a foreign key refers to same thing of another table.


## Question Three:

Given the following table write all the `belongs_to` and `has_many` **and**
`has_many through` associations for models based on the below table
(`Physician`, `Appointment`, and `Patient`)

```ruby
# == Schema Information
#
# Table name: physicians
#
#  id   :integer          not null, primary key
#  name :string           not null


# Table name: appointments
#
#  id   :integer           not null, primary key
#  physician_id :integer   not null
#  patient_id :integer     not null


# Table name: patients
#
#  id   :integer           not null, primary key
#  name :string            not null
#  primary_physician_id :integer

class Appointment < ApplicationRecord
    belongs_to :physician,
        primary_key: :id,
        foreign_key: :physician_id,
        class_name: :Physician

    belongs_to :patient,
        primary_key: :id,
        foreign_key: :patient_id,
        class_name: :Patient
end

class Physician < ApplicationRecord
    has_many :appointments,
        primary_key: :id,
        foreign_key: :physician_id,
        class_name: :Physician

    has_many :Patients,
        primary_key: :id,
        foreign_key: :patient_id,
        class_name: :Patient

end

class Patient < ApplicationRecord
    belongs_to :primary_physician.
        primary_key: :id,
        foreign_key: :patient_id,
        class_name: :Physician

    has_many :appointments,
        primary_key: :id,
        foreign_key: :patients_id,
        class_name: :Appointments
end
