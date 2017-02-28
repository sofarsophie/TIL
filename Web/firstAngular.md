# First Angular

## Setting Up AngularJS

'''
 touch index.html
 open .
'''

Download AngularJS 1.6 [here](http://angularjs.org).

Initialising the html file as an angular

'''
<html lang="en" ng-app>
'''

## Emulating a Hosting Server

Angular: Single-page app (more fluidity)

'''
  python -m SimpleHTTPServer
'''

Go to Chrome
  Enter 127.0.0.1:8000 OR localhost:8000 OR 0.0.0.0:8000
   
## The MVC Architecture


#### Intro to Data Binding

'''
  <h1>Hello, {{name}}!</h1>
  <input type='text' ng-model='name'>
'''

Using conditionals

'''
  <h1>Hello, <span ng-if='name'>{{name}}!</span><span ng-if='!name'>what's your name?</span></h1>
  <input type='text' ng-model='name'>
'''
