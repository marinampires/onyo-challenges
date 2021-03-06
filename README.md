# Onyo Challenge #

Here we have some challenges for the following areas Backend, iOS and Android. Please feel free to enjoy our challenge and let us know if you have any question.

# Backend Challenge #

The main goal of this challenge is to exercise some concepts of API Rest, microservices and integrations. The basic goal is to create two APIs (microservices) using Django Rest Framework or similar web frameworks. These microservices should communicate with each other by JSONs, but should keep their databases separated. Both of them should answer to simple CRUD requests -- Get, Post, Put, Delete. We'll have two APIs, let's consider the first API "Ana" and the second one "Bob". When having a POST to Ana, Ana should perform a request to Bob and will save the answer of Bob on its own database. Bob should have API calls to return random values when its created, so when we have the same input coming from Ana we should have the same answer from Bob. In order to do it, Bob will have to store some data on its own database. The main reason is the needed decoupling between them.

The models, views and business rules may be created at your own criteria. We're interested on the dynamics that these parts will connect to each other.

As a topic we have a few suggestion:
- Bob could serve Postal Code Information (Street, City, State, etc) given a Postal Code it will return information. Ana should consume Bob and propagate its answer.


# Documentation 
This solution is a Django project, which implements 2 microservices as Django applications.
Each one should be deployed on separate servers, since each one use its own database.

Ana is the secretary app. When a contact is created, Ana makes a request to Bob(postman) using the postcode, to retrieve the address.

Bob is the postman app. When it receives a get, retrieve the location associated with the postcode. When the postcode is not found, creates a new location with this postcode and a random address.

Each app has its own settings


## Deploy
Deploy was made in heroku. 
Each app run alone on server, using the DJANGO_SETTINGS_MODULE var, that defines which settings load.

Environment variables needed on server:
### Bob microservice
 * DJANGO_DEFAULT_MODULE: postman => Used on Procfile to load postman wsgi
 * DJANGO_SETTINGS_MODULE: postman.settings => Used to define that postman app must run

### Ana microservice
 * DJANGO_DEFAULT_MODULE: secretary => Used on Procfile to load secretary wsgi
 * DJANGO_SETTINGS_MODULE: secretary.settings => Used to define that secretary app must run
 * POSTMAN_SERVICE_URL: http://marina-onyo-postman.herokuapp.com/locations/ => Postman url for Ana proceed request


## Usage

### Bob
[Locations Endpoint](http://marina-onyo-postman.herokuapp.com/locations)
```bash
	$ curl -H "Content-Type: application/json" http://marina-onyo-postman.herokuapp.com/locations -d '{"address": "Avenida Presidente Vargas", "postcode": "20040010"}'
```
There is a page that can be accessed through: [http://marina-onyo-postman.herokuapp.com/locations/index](http://marina-onyo-postman.herokuapp.com/locations/index)


### Ana
[Contacts Endpoint](http://marina-onyo-secretary.herokuapp.com/contacts)
```bash
	$ curl -H "Content-Type: application/json"  http://marina-onyo-secretary.herokuapp.com/contacts -d '{"postcode": "20040010", "name": "Luciane Pierre", "number":20}' --verbose
```
There is a page that can be accessed through: [http://marina-onyo-secretary.herokuapp.com/contacts/index](http://marina-onyo-secretary.herokuapp.com/contacts/index)


## API Endpoints

### Bob
About the API
[http://marina-onyo-postman.herokuapp.com/locations/docs/](http://marina-onyo-postman.herokuapp.com/locations/docs/)

### Ana
About the API
[http://marina-onyo-secretary.herokuapp.com/contacts/docs/](http://marina-onyo-secretary.herokuapp.com/contacts/docs/)

# TODO #

- [x] Fork challenge
- [x] creates django projects onyo-challenge
- [x] creates app postman
- [x] creates app secretary
- [x] creates base settings
- [x] run both apps local
- [x] create app postman on heroku
- [x] define env_var DJANGO_MODULE_SETTINGS = postman on heroku postman app
- [x] create app secretary on heroku
- [x] define env_var DJANGO_MODULE_SETTINGS = secretary on heroku postman app
- [ ] create command to deploy both apps into heroku
- [x] deploy postman on heroku
- [x] deploy secretary on heroku
- [ ] pull request
- [ ] documentantion


## App Postman
Postal Code Information microservice

- [x] creates model location
- [x] creates model migration
- [x] creates test save location
- [x] creates postman view get
- [x] creates postman view post
- [x] creates postman view delete
- [x] creates postman view update
- [x] creates test view
- [x] configure heroku db
- [x] create a new address when sent a postcode that does not exist
- [ ] loaddata postman
- [ ] fill locations page
- [x] crud page for locations


## App Secretary
Contacts microservice

- [x] creates model contact
- [x] creates model migration
- [x] configure heroku db
- [x] creates test save contact
- [x] creates secretary view get
- [x] creates secretary view post
- [x] define postman service url
- [x] get address information on postman service
- [x] creates secretary view delete
- [x] creates secretary view update
- [x] creates test view
- [x] crud page for contacts
