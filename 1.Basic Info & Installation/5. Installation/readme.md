# Installing PostgreSQL on Windows (Step-by-Step)

This guide explains how to install **PostgreSQL** on a Windows computer.

---

## Step 1: Download PostgreSQL

1. Open your browser.
2. Go to the official PostgreSQL website:
   https://www.postgresql.org/download/windows/
3. Click **Download the Installer**.
4. You will be redirected to the **EnterpriseDB** download page.
5. Download the latest version of PostgreSQL for Windows.

---

## Step 2: Run the Installer

1. Locate the downloaded file (usually in the **Downloads** folder).
2. Double-click the installer file (example: `postgresql-16.x-windows-x64.exe`).
3. Click **Next** to start the installation.

---

## Step 3: Choose Installation Directory

1. Select the folder where PostgreSQL will be installed.
2. The default location is usually:

```
C:\Program Files\PostgreSQL\version
```

3. Click **Next**.

---

## Step 4: Select Components

Choose the components you want to install.

Common components include:

* PostgreSQL Server
* pgAdmin (database management tool)
* Command Line Tools
* Stack Builder

Keep the default selection and click **Next**.

---

## Step 5: Set Data Directory

Choose the folder where PostgreSQL will store database files.

Usually the default directory is fine.

Click **Next**.

---

## Step 6: Set Password for Database Superuser

You must create a password for the **postgres** user.

Example:

```
Username: postgres
Password: your_password
```

Remember this password because you will need it to access the database.

Click **Next**.

---

## Step 7: Select Port Number

The default PostgreSQL port is:

```
5432
```

Keep the default port unless you need a different one.

Click **Next**.

---

## Step 8: Choose Locale

Select the default locale for the database.

You can keep the **default locale** and click **Next**.

---

## Step 9: Install PostgreSQL

1. Review the installation summary.
2. Click **Next** to start installation.
3. Wait for the installation process to finish.

---

## Step 10: Finish Installation

1. Click **Finish** after installation is complete.
2. You may be asked about **Stack Builder** (optional).
   You can skip it for now.

---

## Step 11: Open pgAdmin

After installation:

1. Open the **Start Menu**.
2. Search for **pgAdmin**.
3. Open **pgAdmin**.
4. Enter the password you created earlier to connect to PostgreSQL.

---

## Verify Installation

You can test PostgreSQL using the command line.

Open **Command Prompt** and run:

```bash
psql -U postgres
```

Enter your password. If the PostgreSQL shell opens successfully, the installation worked.

---

## Conclusion

PostgreSQL is now installed on your Windows system.
You can manage databases using **pgAdmin** or the **psql command line tool**.
