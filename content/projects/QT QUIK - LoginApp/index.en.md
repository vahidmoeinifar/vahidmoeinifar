---
weight: 1
title: "QT QUIK - LoginApp"
date: 2020-03-06T21:29:01+08:00
lastmod: 2020-03-06T21:29:01+08:00
draft: false
author: "Vahid Moeinifar"
description: "A QT Quick application with Sqlite database for user login."
images: []
resources:
- name: "featured-image"
  src: "featured-image.png"

tags: ["installation", "configuration"]


lightgallery: true

toc:
  auto: false
---

Discover what the Hugo - **LoveIt** theme is all about and the core-concepts behind it.

<!--more-->

### Description

A straightforward QT Quick application with an SQLite database for user login is implemented. In this application, during the initial launch, the user is prompted to set up an admin username and password. Once configured, the admin can log in and create additional user accounts. This login application is designed specifically for industrial machines, enabling the admin to create multiple users with distinct permissions to operate the machines through the application. Furthermore, the application features a user manager section that allows the admin to modify or remove information for other users. An additional functionality provided by the application is the ability to recover a forgotten password by using either the username or email associated with the account.

This application utilizes a single table in the database, containing fields for the user's name, hashed password, and email. Users have the ability to retrieve their password through a simple method. When triggered, a unique 4-digit number is generated and displayed in the console. Users can employ this code to recover their password. The handling of this 4-digit code is flexible and can be managed as per your requirements. For instance, you have the option to send the retrieved code to the user's email at a later time. During the initial setup, users are required to sign up and create a new account.


[Click here to see project on github](https://github.com/vahidmoeinifar/QT-Login-App)


{{< admonition note "To see the project on github: " >}}

 

You can see here a sample code of the new user register function:
```bash

QString DB::registerNewUser(QString uname, QString pword, QString pword2, QString email, int roleId)
{
    QString hashedPass = hashFunction(pword);
    QString ret = validateRegisterCredentials(uname, pword, pword2, email);
    if ("" == ret){
        QSqlQuery queryInsert;
        queryInsert.prepare("INSERT INTO UserDetails (username, password , roleId, email) VALUES(? ,? ,? ,? )");
        queryInsert.bindValue(0, uname);
        queryInsert.bindValue(1, hashedPass);
        queryInsert.bindValue(2, roleId);
        queryInsert.bindValue(3, email);
        queryInsert.exec();

        if ( queryInsert.next())
            return "";
        else
            return m_modelUserDetails->lastError().text();
    }
    else
        return ret;

    if (uname == "admin")
        return "You can not use admin as username. It's reserved.";
}
```

{{< /admonition >}}


![LoginApp](/assets/img/loginApp.png "LoginApp")


