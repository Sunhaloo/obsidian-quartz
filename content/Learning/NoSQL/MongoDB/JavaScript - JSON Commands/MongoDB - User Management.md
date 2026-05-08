---
id: User Management
aliases: Creation - Modification - Deletion  and Grant Permissions ( User Management )
tags:
  - uni
  - uom
  - db
  - NoSQL
author: S.Sunhaloo
date: 2025-03-31
status: HOLD
---

## List of Contents

- [[#Creation of User]]
	- [[#Create A Simple User]]

---


>[!NOTE]
>Because I am on Linux; I **will** have to *create* a user to be able to [[MongoDB Document-Based Database Introduction#To Authenticate or Not To Authenticate | authenticate]] and use commands.
>
>If I don't authenticate at all... When I try to run commands like `db.getUsers()` ( *for example* ), I get errors like this $\downarrow$:
>
>```console
>MongoServerError[Unauthorized]: not authorized on admin to execute command 
>```
>
>But if you have read the previous note / file that I made called '[[MongoDB Document-Based Database Introduction]]'; then you know what I am talking about!
>
>>[!NOTE] Additionally
>>As I don't really know what I am doing because everything is so new... Instead of writing a general '*Resource*' section here.
>>
>>I will be providing the **resources** for each *method* at each *heading*.
>>
>
>BTW I have **already** created the administrator user so that I can *actually* use these commands!
>Please go to the note / file mentioned above $\uparrow$ if you are on ( _Arch_ ) **Linux**.
>

>[!INFO] General Resource
>- https://www.mongodb.com/docs/mongodb-shell/reference/methods/#user-management-methods

# Creation of User

>[!INFO] Resource
>- Official Documentation:
>	- https://www.mongodb.com/docs/manual/reference/method/db.createUser/
>	- https://www.mongodb.com/docs/manual/tutorial/manage-users-and-roles/
>- Others:
>	- https://www.geeksforgeeks.org/create-user-and-add-role-in-mongodb/

## What is a 'Role' and 'Privilege'.

>[!TIP] What is `role`?
>
>>[!INFO] Built-In Roles
>>Here is the official documentation about what values the `role` *parameter* can take $\downarrow$
>>
>>- https://www.mongodb.com/docs/manual/reference/built-in-roles/

## Create A Simple User

We are now going to **create** a *simple* user that does **not** have any *roles*.

```json
```

>[!WARNING]
>Every time we are going to be **creating** a user or using *admin* specific commands. We **need** to first switch to the 'admin' database!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/channel/UCMkQZsuW6eHMhdUObLPSpwg
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!