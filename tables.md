# Quais são as tabelas

Table: `areas`  
Description: List of the UFBA's areas of knowledge  
Columns: 
* `id`
* `name`
* `description`  

Table: `course_class_offers`  
Description: Relation many-to-many between the tables courses and discipline_class_offers    
Columns: 
* `id`
* `course_id`
* `discipline_class_offer_id`  
  
Table: `course_disciplines`  
Description: Relation many-to-many between the tables courses and disciplines    
Columns: 
* `id`
* `semester`
* `nature`
* `course_id`
* `discipline_id`
* `created_at`
* `updated_at`

Table: `courses`  
Description: List of the courses offered by UFBA  
Columns:
* `id`
* `name`
* `code`
* `created_at`
* `updated_at`
* `curriculum`
* `area_id`

Table: `discipline_classes`  
Description: Relation many-to-one of the table disciplines  
Columns:
* `id`
* `discipline_id`
* `class_number`

Table: `discipline_class_offers`  
Description: Relation many-to-one of the table discipline_classes  
Columns:
* `id`
* `discipline_class_id`
* `vacancies`

Table: `disciplines`  
Description: List of the disciplines offered by UFBA  
Columns:
* `id`
* `code`
* `name`
* `created_at`
* `updated_at`
* `curriculum`
* `load`

Table: `pre_requisites`  
Description: List of the pre-requisites of the disciplines offered by UFBA  
Columns:
* `id`
* `pre_discipline_id`
* `post_discipline_id`
* `created_at`
* `updated_at`

Table: `professor_schedules`  
Description: Relation many-to-many between the tables schedules and professors  
Columns:
* `id`
* `schedule_id`
* `professor_id`

Table: `professors`  
Description: List of the professors teaching at UFBA  
Columns:
* `id`
* `name`

Table: `schedules`  
Description: List of the schedules of a disciplines class  
Columns:
* `id`
* `day`
* `start_hour`
* `start_minute`
* `discipline_class_id`
* `end_hour`
* `end_minute`
* `first_class_number`
* `class_count`
