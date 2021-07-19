## Question One

What are the disadvantages of adding an index to a table column in a database?

- we need to allocate extra space to store the index


## Question Two

Given the following table write all the `belongs_to` and `has_many` associations
for models based on the below table (`User`, `Enrollment`, and `Course`)

```ruby

# == Schema Information
#
# Table name: users
#
#  id   :integer                not null, primary key
#  name :string                 not null


# Table name: enrollments
#
#  id   :integer                not null, primary key
#  course_id :integer           not null
#  student_id :integer          not null


# Table name: courses
#
#  id   :integer                not null, primary key
#  course_name :string          not null
#  professor_id :integer        not null
#  prereq_course_id :integer    not null
```


class User < ApplicationRecord
    has_many :enrollements,
    primary_key: :id,
    foreign_key: :course_id,
    class_name: :Enrollment

    has_many :courses,
    primary_key: :id,
    foreign_key: :professor_id
    class_name: :Course
end

class Enrollment < ApplicationRecord
    belongs_to :course,
    primary_key: :id,
    foreign_key: :course_id,
    class_name: :Course

    belongs_to :student,
    primary_key: :id,
    foreign_key: :student_id,
    class_name: :User
end

class Course < ApplicationRecord
    belongs_to :professor,
    primary_key: :id,
    foreign_key: :professor_id,
    class_name: :User

    belongs_to :prereq_course,
    primary_key: :id,
    foreign_key: :prereq_course_id,
    class_name: :Course
end

## Question Three

Given all possible SQL commands order by order of query execution. (SELECT,
DISTINCT, FROM, JOIN, WHERE, GROUP BY, HAVING, LIMIT/OFFSET, ORDER).

select
distinct
from
join
where
group by
having
order
limit/offset