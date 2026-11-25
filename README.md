# Smart Clinic Managemenrt System

A Spring Boot application uses both MVC and REST controllers. Thymeleaf templates are used for the Admin and Doctor dashboards, while REST APIs serve all other modules. The application interacts with relational DB MySQL (for patient, doctor, appointment, and admin data) and NoSQL Document DB MongoDB (for prescriptions). All controllers route requests through a common service layer, which in turn delegates to the appropriate repositories.

# Architecture
```text
+-----------------------------------+    +---------------------------------------------------+

|            Dashboards             |    |                    RESTModules                    |
| +---------------+ +-------------+ |    | +--------------+ +--------------+ +-------------+ |
| |AdminDashboard | |DoctorDashb. | |    | | Appointments | |PatientDashb. | |PatientRecord| |
| +---------------+ +-------------+ |    | +--------------+ +--------------+ +-------------+ |
+-----------------+-----------------+    +-------------------------+-------------------------+

                  | uses                                           | uses JSON API
                  v                                                v
+--------------------------------------------------------------------------------------------+

|                                       SpringBootApp                                        |
|                                                                                            |
|         +-----------------------+                        +-----------------------+         |
|         | Thymeleaf Controllers |                        |   REST Controllers    |         |
|         +-----------+-----------+                        +-----------+-----------+         |
|                     |                                                |                     |
|                     +--------------> +---------------+ <-------------+                     |
|                              calls   | Service Layer |   calls                             |
|                                      +-------+-------+                                     |
|                                              |                                             |
|                            +-----------------+-----------------+                           |
|                       uses |                                   | uses                      |
|                            v                                   v                           |
|               +------------------------+           +--------------------+                  |
|               |   MySQL Repositories   |           | MongoDB Repository |                  |
|               +------------+-----------+           +---------+----------+                  |
|                            | accesses                        | accesses                    |
|                            v                                 v                             |
|                +----------------------+            +--------------------+                  |
|                |    MySQL Database    |            |  MongoDB Database  |                  |
|                +-----------+----------+            +---------+----------+                  |
|                            |                                 |                             |
|                            v                                 v                             |
|                +----------------------+            +--------------------+                  |
|                |     MySQL Models     |            |   MongoDB Model    |                  |
|                | (JPA Entities:       |            | (Document:         |                  |
|                |  Patient, Doctor,    |            |  Prescription)     |                  |
|                |  Appointment, Admin) |            +--------------------+                  |
|                +----------------------+                                                    |
+--------------------------------------------------------------------------------------------+
```
