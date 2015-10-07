---
layout: post
title:  "The Interface Segregation Principle: A SOLID Software Principle"
date:   2015-10-07 15:23:36
categories: interface segregation principle SOLID software design 
---
Why should your software depend on things that you don't need? According to the Interface Segregation Principle, it shouldn't.

The Interface Segregation Principle (ISP) is one of the 5 SOLID prinicples in Object-oriented software design. This principle deals with the problem of having "fat" interfaces that include too many methods. In order to adhere to this principle, you want your interfaces to isolate specific behavior that your client will depend on. In other words, your client classes that use an interface should only depend and implement the methods that it will need.   

Basically, what ISP can be boiled down into is this: 

> "Don't depend on things you don't need"

To kind of help illustrate what I'm talking about here, I'll give a simple example in Java using a car example. I think using a car as an example is a great way to illustrate this, because if you think about it, a car has a lot of moving parts. So, imagine that we have a `Car` class that uses a generic interface called `Vehicle`, like so:

    public interface Vehicle {
        public void turnOn();
        public void turnOff();
        public void accellerate();
        public void decellerate();
        public void startRadio();
        public void changeStation();
        public void ejectCD();
    } 

    public class Car implements Vehicle {
        public void turnOn() {
            // implementation 
        }
        public void turnOff() {
            // implementation
        }
        public void accellerate() {
            // implementation
        }
        public void decellerate() {
            // implementation
        }
        public void startRadio() {
            // implementation
        }
        public void changeStation() {
            // implementation
        }
        public void ejectCD() {
            // implementation
        }
    }

The thing to look at here is the fact that there's a lot going on in the Vehicle interface. What if you needed to create a car that doesn't have a radio but still implements the Vehicle interface? You would be forced to implement the `startRadio()`, `changeStation()`, and the `ejectCD()` functions, and thus, violating the Interface Segregation Principle. Don't you think that we could break these methods up in to more isolated behaviors? Most certainly! Lets see how we might want to do this.

    public interface Startable {
        public void turnOn();
        public void turnOff();
    }
    public interface CarRadio {
        public void startRadio();
        public void changeStation();
        public void ejectCD();
    }
    public interface Moveable {
        public void accellerate();
        public void decellerate();
    }
    
    public class Car implements Startable, CarRadio, Moveable {
        public void turnOn() {
            // implementation 
        }
        public void turnOff() {
            // implementation
        }
        public void accellerate() {
            // implementation
        }
        public void decellerate() {
            // implementation
        }
        public void startRadio() {
            // implementation
        }
        public void changeStation() {
            // implementation
        }
        public void ejectCD() {
            // implementation
        }
    }

This is a lot better, and the names of the interfaces should explain what is happening in the client. By having these methods prototyped in separate interfaces, you have a bit more flexibility in how you can later implement different types of vehicles with different behaviors based on what the client needs.

 
