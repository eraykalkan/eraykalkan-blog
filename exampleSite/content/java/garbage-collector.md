---
date: "2020-04-04"
tags: ["java", "jvm", "memory","memory management", "heap", "stack", "metaspace", "garbage","garbage collector","collector","garbage collection"]
title: "Java Memory Management and Garbage Collection in Java"
---

Data allocation and de-allocation in various programming languages are among the most challenging and important tasks of course.
In most of older programming languages like C and C++, you will need to handle those recycled data by yourself.
However, Java has a built-in actor that does the job for you (at least in most cases). In other words, you don't need to worry about destroying objects in memory.

Think Garbage Collector in Java as a daemon thread. Deamon thread is a thread that does not prevent the JVM from terminating/exiting when the program finishes. It just keeps running.
Garbage collector basically does this:
Periodically checks heap memory and frees it up from unreachable (garbage) objects.
By saying an unreachable object we mean an object that is no longer referenced by any line or any part of the program.

In order to fully understand what garbage collection is, first we need to have a bit understanding of Java Memory Management.

# Java Process Memory Model

Let's start with the birth and death of an object inside the JVM and memory model of Java.
When the JVM is launched, it allocates memory for the process in operating system. 
The allocated memory and this process (JVM in this case) include:
Heap, Meta space, JIT code cache, stack, and shared libraries.

## Heap Memory

The heap memory is used to store reference types (objects), class instances, arrays which are run-time data.
The heap is created when JVM starts. It can dynamically increase and decrase its size during run-time.
We can specify the heap size using -Xms VM option. Also we can specify maximum heap size with the -Xmx option.

## Non-Heap Memory

Non-heap memory is created by JVM when it starts up. Non-heap memory stores most importantly interned Strings, run-time constant pool,
field and method data, code for constructors, code for methods.

## Other Memory

It is intended to be used by JVM to store JVM code itself. In addition, JVM internal structures, loaded profiler agent code, and data.

# Java Heap Memory Structure

Heap memory consists of various areas, and it is split into two areas; "Young Generation" and "Tenured" space.

1) Young Generation: It is also called New Space, is divided into two parts. "Eden" and "Survivor" Space.
    - Eden : The first place that an object is born. When an object is created, memory will be allocated from the Eden Space.
    - Survivor Space : In this space, there are objects that have survived Young garbage collection / minor garbage collection because they can be still needed by the program or not marked to be collected yet. This space is divided into two parts (spaces) called S0 and S1.

 2) Tenured Space: Also called Old Generation Space. The objects that reached to a certain amount of maturity in memory, or lost its appeal to the program; will be moved to "Tenured Space". More formally, the objects which have reached to a max treshold during minor garbage collection will be marked for death in tenured space. They become eligible to be collected by garbage collector later.
 
 # Java Memory Models

## Permanent Generation (Prior to Java 8, it is replaced by Metaspace since Java 8)

This generation contains application metadata that is needed by JVM. This generation is loaded by JVM at runtime according to the classes used by Java application and it also contains standard Java library (Java SE) classes and methods. Objects in this generation are garbage collected in a full garbage collection.

## Metaspace

This memory is part of the native memory. It is not a part of heap. By default it does not have an upper limit. It used to be called "Permanent Generation" until Java 8.
The duty of this memory is to store class definitions that are loaded by class loaders. By saying it doesn't have upper limit it is meant that it is designed to grow dynamically in order to prevent out of memory errors. If it exceeds physical memory, the OS will use virtual memory. However, this will affect applcation performance of course because swapping between memories (from virtual to physical and vice versa) is going to cost us a time. The JVM options “-XX:MetaspaceSize” and “-XX:MaxMetaspaceSize” are used to set the size of metaspace.

## Code Cache

The interpreter which is responsible for interpreting the byte code and convert it into machine understandable code in JVM uses this cache. The JIT (Just In Time) compiler, compiles the most frequently used code to machine code and stores it in code cache.

## Method Area

This area is a part of permanent gen and it stores class structure (runtime constants, static variables), code for methods and constructors.

## Memory Pool

These are created by JVM memory managers. It serves the purpose of providing a pool of immutable objects. Memory pool may belong to Heap or Perm gen according to JVM memory manager implementation.

## Runtime Constant Pool

Contains class runtime constants and static methods. It is a part of the method area.

## Java Stack Memory

Stack memory is based on thread execution. It is used for execution of a thread. It contains method related values, references to other objects in the heap which are getting referred from the method.

# Garbage Collection


Garbage collection as stated in the very beginning of this blog, is the process of freeing space in the heap in order provide new space for new objects. It is basically a thread responsible for running in the background and checking for the objects in memory to discover the ones that are no longer needed, no longer referenced by any part of the program. Unreferenced objects are deleted from memory.
One of the most important feature of Java is automatic garbage collection. It is open to debate however. If you are working on a critical real-time systems, automatic garbage collection can cause a lot of trouble.

Mainly this process involves in three steps:

    - Marking: In this first step, garbage collector identifies which objects are referenced and which are not.
    - Normal Deletion: Garbage collector deletes unusued / unreferenced objects and allocates space for other newly created objects.
    - Deletion with compacting: After deletion takes place, all survived objects are moved together in order to increase memory allocation process for newer objects.
    
As we have mentioned above, the JVM reserves a separate thread (a daemon thread) to perform garbage collection and garbage collection in Java consists of minor GC and major GC.

Let's start with minor GC.

At first, the survivor space and the tenured space are both empty. If JVM is unable to get memory from eden space, minor GC is initiated. During this, the objects that are not reachable by the program are marked to be collected by garbage collector. After that the JVM picks one of the survivor spaces S0 or S1. Then the JVM copies reachable objects to selected survivor space and icrements the reachable objects age by one. If the moved objects won't fit into the selected survivor space, they are moved to tenured space. The name of this process is called "premature promotion".

There is a JVM option to specify the object age threshold for the objects in tenured space "MaxTenuringThreshold". Default value is 15.
We can deduct that minor GC reclaims memory from Young Generation Space. Minogr GC is a "stop the world" process however, don't let the naming fool you. That application pause is so negligible that it isn't even noticed since it is performed with threads.

If the minor GC is performed many times, naturally it will result in filling up the Tenured Space and it is going to its own garbage collection. Consequently, the JVM will trigger a major GC. It can also be called full GC. During major GC, the JVM reclaims memory from "Meta Space". If there are no objects in the heap, the loaded classes will be removed from meta space.

There are several ways that the Garbage Collection is triggered:

    - JVM decides (if tenured space is not enough)
    - If we call it manually (System.gc(), Runtime.getRuntime().gc()) however, this does not guarantee that it will perform GC immediately. It is just a suggestion that JVM should trigger it.
    - If "MaxMetaspaceSize" JVM option is set and there isn't adeaquate space to load new classes, then major GC is triggered by JVM

There will be detailed topics about Garbage Collection in Java in near future. So, stay tuned!