---
Created: 2023-07-17 10:36
aliases:
  - ioc
  - inversion of control
---

## Description
---

### Examples:

Using python to demonstrate the problem

```python

class EmailService():

	def __init__(self, user_id):
		self.user_id

	def send_email(address):
		...


class UserService():

	def __init__(self, user_id):
		self.email_service = EmailService(user_id)

```

The hidden problem of the above code is EmailService is directly initialized in the UserService.  
The problem rises when UserService needs to initialize lots of services.  
E.G

```python
class UserService():
	def __init__(self, ... lots of parameters to put in ...):
		self.email_service = EmailService()
		self.notification_service = ...
		self.streaming_service = ...
		...
```

This causes the UserService class becomes way too big and it violates the SOLID rule,  
keep modifying the same piece of code. It is a bad design.

### How to Solve This ?

The easiest way is to separate the responsibility of initializing dependencies.  
What we are going to do, is move all the services out of the  initialize function.

```python

class UserService():
	def __init__(self, email_service, notification_service, streaming_service, ...):
		self.email_service = email_service
		...

def main():
	email_service = EmailService()
	notification_service = NotificationService()
	...
	user = UserService(email_service, notification_service, ...)

```

This is way cleaner, since UserService doesn't need to handle the responsibility of initializing these dozen of objects, and it's  
way easier to control the steps of initializing.

### We Can Do it Better

It's not necessary in python, but it's definitely important in static type languages.  
The caller or user needs to know how to inject the service instances into the UserService.  
That is what kind of objects do we need to inject in order to use UserService.  
This is where Interfaces kicks in.

```python
from abc import ABC, abstractmethod

class IEmailService(ABC):

	@abstractmethod
	def send_email(self):
		raise NotImplimentedError

class INotificationService(ABC):
	...


class UserService():

	def __init__(self, email_service: IEmailService, notification_service: INotificaionService):
		...

```

This makes the caller, whoever tries to use UserService, understands how to initialize this object.  
By looking in to the type hint. The another reason why using interfaces is that perhaps there are more than  
one kind of email service. e.g Google, Yahoo, Microsoft …. These service contains their unique apis.  
Therefore interface is a good way to restrict the api interface or at least implement it, in order to use UserService.

Such as:

```python

class GoogleMailService(IEmailService):

	def send_email(self):
		# implementation detail, this method should be implemented, restrict by IEmailService
		...

	def others_blah_blah_blah(self):
		...

```

Go, on the other hand, supports interface natively, so it's more natural to do this kind of stuff.

```go
type IEmailService interface {
	SendEmail(address string) nil
}

type GoogleEmailService struct {}
func (g GoogleEmailService) SendEmail(address string){}

type UserService struct {
	emailService IEmailService
}

// Its better to use a separate init function in go
func InitUserService(emailService IEmailService) UserService{
	return UserService{
		emailService: emailService,
	}
} // indicates that instance must satisfies IEmailService

func main(){
	mailService := GoogleEmailService{}
	userServuce := InitUserService(emailService)
	... do stuff
}

```

## Still there is One step a way to Perfection

We still need ….. some where in order to initialize these objects.  
When the number of  dependency becomes huge. It is a problem and even there are dozens of Services  
that needs this kind of initialization step. How do we fix it ?  
Thank god there are several ways to go. The most famous one, [[Dependency Injection]]
