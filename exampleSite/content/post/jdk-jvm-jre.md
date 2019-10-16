---
date: "2019-10-16"
tags: ["jdk", "jre", "jvm"]
title: "JDK, JVM ,JRE - The Three Musketeers"
---

# JDK, JVM, JRE - The Three Musketeers

You may or may not have heard of those abbreviations and they are often neglected by most developers. You can tell yourself what you are supposed to do with that information or what is going to change on your life if you know what they do or how they work.

However, knowing those things or at least having a little bit idea of why they are here can be life saving in some situations.

JDK, JVM and JRE all serve different purposes and there are some points that they sound like they are doing similar things.

Let's clear up that confusion and have a grasp on core concepts of Java.

## JVM - Java Virtual Machine

Usually people start by explaining what JDK is then proceed with JVM, but there is this term called **"Platform Independency"** which once was (maybe still is) motto of Java Language. The term is abused so much that everyone has forgot about why Java is also so popular and powerful. It's been an **open-source** language for quite some time. Things are changing however it is not this post's topic.

Enough with the chit chat. Java Virtual Machine is what makes Java platform dependent. Let me explain how;
In order a computer to **run** a program, first the computer needs to understand what's going on and computers talk machine language. This is where the JVM comes in play. JVM transforms/converts byte code to machine understandable code. It also provides some vital functions of the language which involve in memory management, security, garbage collection.
JVM is also configurable and customizable according to needs of the program that are being developed. Beware: Your Java program lives in JVM and has the boundaries that are set by JVM.
Since it is basically a virtual machine, it is independent from OS and hardware on the computer it is working.

Although it makes Java language **platform independent**, he himself is very much **platform dependent**. It has different installers for different platforms.

## JDK - Java Development Kit

If you are a bit interested in programming especially game programming, you already know what a development kit does. A development kit is basically a required set of development tools, binaries, executables that you need when you are doing the actual **"developing"** job, and Java Development Kit is no exception.
It provides the tools, executables and libraries a developer needs to **compile and execute** a Java program. JDK is also platform dependent and has separate installers for different operating systems. JDK contains JRE and debugger and also core classes of Java.

## JRE - Java Runtime Environment

A runtime environment in general means a natural habitat for a program or a software to run. Java Runtime Environment is responsible for providing a platform for Java programs. It consists of JVM, class libraries, class loader. One thing you need to know is that if you want to execute a Java program, you should have JRE. JDK is not a must to run a Java program.

# JVM vs JDK vs JRE - Their Differences

1. JVM is the virtual machine that makes Java platform independent.
2. JDK and JRE contains JVM.
3. JDK is the development kit that has the necessary tools.