---
Created: 2022-12-12 13:30
url:
alias: [django, commands]
---

Card Link:  
Tags: #Django #Command

---
- `python manage.py shell_plus`  
Activate Ipython shell, with django models, views imported

- `python manage.py shell_plus --print-sql`  
Activate Ipython shell, django models and show sql related information while using ORM.

- `python manage.py show_urls`  
Show actual url for django url mapping

- `python manage.py makemigrations -n "migration_name"`
- `python manage.py migrate`
- `python migrate <app_name> <migration number or full name>`  
Set migration back to certain migration number

- `python manage.py createsuperuser`  
Create superuser if django permission application is set.

- `python manage.py runscript --force <script name>`  
Manual load specific script  
This is a customized script 



