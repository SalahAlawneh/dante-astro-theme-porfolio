---
title: Thread Safe Singleton
excerpt: The Singleton Pattern is a design pattern used to ensure that only one instance of a class is created throughout the lifecycle of an application.
publishDate: 'December 15 2024'
seo:
  image:
    src: '/post-1.jpg'
    alt: A person standing at the window
---

![A person standing at the window](/singleton.jpg)

[//]: # (**Note:** This post was created using Chat GPT to demonstrate the features of the _[Dante Astro.js theme functionality]&#40;https://justgoodui.com/astro-themes/dante/&#41;_.)

The Singleton Pattern is a design pattern used to ensure that only one instance of a class is created throughout the lifecycle of an application.

## When Do We Need a Singleton?
You might wonder, “Why would I want only one instance of a class?”

A common example is a database connection class. In most applications, you only need a single instance to manage your database connection. Creating multiple instances could lead to inefficiencies or errors, so the Singleton pattern is a perfect solution for this scenario.

## How to Write a Singleton?
The Singleton pattern is one of the simplest design patterns. Here’s a basic example of how it can be implemented in Java:
```
public class Database {
    // Create a private static instance of the class to hold the single instance
    private static Database database;

    // Private constructor to prevent instantiation from outside
    private Database() {
    }

    // Public static method to get the single instance
    public static Database getInstance() {
        // If the instance is null, create a new instance
        if (database == null) {
            database = new Database();
        }
        // Return the single instance
        return database;
    }
}
```
This implementation works well in a single-threaded environment. But what happens in a multi-threaded environment?

## The Multi-Threading Problem
In a multi-threaded environment, two or more threads could call getInstance() at the same time. If the database instance is null, both threads might enter the if (database == null) block simultaneously. This could result in two separate instances being created, which violates the Singleton pattern's goal of having only one instance.

## How to Create a Thread-Safe Singleton?
There are multiple ways to make a Singleton thread-safe, but one of the cleanest and most efficient methods is to use a static inner helper class. This approach is often called the Bill Pugh Singleton Pattern. Here’s how it looks:
```
public class Database {
    // Private constructor to prevent instantiation from outside
    private Database() {
    }

    // Static inner class to hold the Singleton instance
    private static class DatabaseHelper {
        // Create a static final instance of the Singleton class
        private static final Database INSTANCE = new Database();
    }

    // Public static method to get the Singleton instance
    public static Database getInstance() {
        // Return the Singleton instance from the inner class
        return DatabaseHelper.INSTANCE;
    }
}
```

## Why Is This Thread-Safe?
The static inner class (DatabaseHelper) is not loaded into memory until it is first accessed. This ensures lazy initialization, and the Java ClassLoader guarantees that the instance is created in a thread-safe way without requiring synchronization.

## Conclusion
The Singleton pattern is a simple yet powerful design pattern, and the Bill Pugh Singleton Pattern is an elegant and efficient way to implement it in a multi-threaded environment. Whether you’re working on a database class, a logging utility, or other components that require a single instance, the Singleton pattern ensures consistency and optimal resource usage.

Happy coding!