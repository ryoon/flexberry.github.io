--- 
title: Subsystem powers 
sidebar: ember-flexberry-security_sidebar 
keywords: Flexberry Security 
toc: true 
permalink: en/efs_right-manager-module.html 
lang: en 
autotranslated: true 
hash: 73cdc78a1ccf3df305dba3fcfa167dee28b6c04230ff05b7c55c14a78144cfd6 
--- 

## Subsystem powers 

To ensure information security the system implements the separation of user rights. This task is performed by the subsystem powers. 

`Подсистема полномочий` is [plug-in functional module of the application](fd_prototype-creation.html) that is generated when pomoechnye Flexberry. 

### the structure of the subsystem powers 

The system selects the subjects (users and roles), objects, and operations performed by subjects on objects. 

Under `операцией` refers to either a standard action on an object (viewing a specific object, viewing the object list, create, edit, delete) or specific (system start-up, the execution of the business transaction). Subsystem authority determines whether users have the right to perform operations on objects. 

### Entities subsystem powers 

The main actors are the users of the system. Roles are used to simplify administration. Each user of the system can be assigned one or more roles in relation to it. `Ролью` called one of the scenarios of the user experience with the system. 

### the Right of access to the subsystem powers 

Customize access rights to objects at the level of their classes. This means that if you have permission to execute any operation for the specified class the user can implement it on any object of that class. 

A valid user's rights to perform the operation on the object consist of rights assigned to the roles to which it belongs, and of the rights assigned to him individually. 

It is also possible to add or remove roles, assign them to users and set privileges to perform operations of browsing, adding, modifying, and deleting [over objects](efs_security-rights-objects.html) of the specified classes. 

### features of use of the subsystem powers 

[Engine powers Web-applications](fa_right-manager.html) does not require third-party services and comes along with the application in the generation of [Flexberry Designer](fd_landing_page.html). 

For windows applications is used [Service authority Flexberry Rights](efs_security-legacy-services.html). 

To configure the credentials can be used [Security Console](efs_security-console.html). 



{% include callout.html content="Переведено сервисом «Яндекс.Переводчик» <http://translate.yandex.ru>" type="info" %}