# Database Authentication Project

## Overview
This project focuses on implementing database authentication, allowing access only to valid users. The system utilizes a database named `user_details` to store user names and encrypted passwords. Instead of storing raw passwords, the database stores encrypted versions. When attempting to access the API, the system checks for the user's presence in the `user_details` database. If the user is found, access is granted; otherwise, access is denied.

## Project Components

### Controller
In the controller, a class named `UserDetailsController` is created. This class holds a reference to the service class called `UserDetailsService`. All URL mappings are defined in this controller.

### DAO (Data Access Object)
Within the DAO layer, a class called `UserDetailsRepo` is implemented, extending `CrudRepository`. This class includes a Hibernate query to fetch user details for a given username.

### Entity
In the Entity layer, a class named `UserDetails` is defined. This class encapsulates the properties or attributes of the `user_details` database.

### Security
The security class comprises three classes: `SecurityConfig`, `CustomUserDetailsService`, and `CustomUser`. In `SecurityConfig`, there is a `DaoAuthenticationProvider` responsible for authenticating users. When a user attempts to log in with a username and password, control is transferred to `DaoAuthenticationProvider`. The `loadUserByUsername` method is called, which, in turn, invokes the corresponding method in `CustomUserDetailsService`. In this method, a reference to `UserDetailsRepo` is created to check if the username is present in the database. If the data is found, the `CustomUser` class is invoked, setting the username and password of the user stored in the database.

### Service
In the service layer, an interface named `UserDetailsService` and a class named `UserDetailsImp` are implemented. In `UserDetailsImp`, two methods are provided: one for adding user details to the `user_details` database and the other for retrieving information from the database.

## Technology Stack

- Spring Framework: 3.2.2
- JDK Version: 17
- Database: MySQL
- Build Tool: Maven
