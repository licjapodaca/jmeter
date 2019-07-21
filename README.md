# **Apache - JMeter**
Repository to practice the using of JMeter, an opensource project for many different of tests, like Stress, Performance and Load tests.

- [**Apache - JMeter**](#apache---jmeter)
- [**Using JMeter for Different Tests**](#using-jmeter-for-different-tests)
	- [**How to install Apache JMeter**](#how-to-install-apache-jmeter)
		- [**Pre-requisites**](#pre-requisites)
		- [**Installation**](#installation)
		- [**Post-Installation**](#post-installation)
	- [**Types of Tests**](#types-of-tests)
		- [**Smoke Test**](#smoke-test)
		- [**Load Test**](#load-test)
		- [**Stress Test**](#stress-test)
		- [**Spike Test**](#spike-test)
		- [**Endurance Test**](#endurance-test)
	- [**Test Plan**](#test-plan)
		- [**Test Plan Structure**](#test-plan-structure)
		- [**Elements of a Test Plan**](#elements-of-a-test-plan)
			- [**Thread Group**](#thread-group)
				- [**How to add a Thread Group**](#how-to-add-a-thread-group)
				- [**Properties of a Thread Group**](#properties-of-a-thread-group)
				- [**Configuration Elements**](#configuration-elements)
				- [**Controllers**](#controllers)
				- [**Timer**](#timer)
				- [**Assertion**](#assertion)
			- [**Listener**](#listener)
		- [**Execution Order and Rules**](#execution-order-and-rules)
			- [**Types of Elements in the Tree Structure**](#types-of-elements-in-the-tree-structure)
			- [**Execution Order**](#execution-order)
			- [**Configuration Elements Rules**](#configuration-elements-rules)
			- [**General Rules**](#general-rules)
		- [**Test Fragments**](#test-fragments)
	- [**Important Application Performance Metrics**](#important-application-performance-metrics)
- [How to record actions in JMeter](#how-to-record-actions-in-jmeter)
	- [**Http(s) Test Script Recorder**](#https-test-script-recorder)
	- [**BlazeMeter Chrome Extension**](#blazemeter-chrome-extension)
- [**JMeter Distributed Mode**](#jmeter-distributed-mode)
	- [**JMeter Distributed Mode Architecture**](#jmeter-distributed-mode-architecture)

# **Using JMeter for Different Tests**

## **How to install Apache JMeter**

### **Pre-requisites**

- Install Java SE JDK v8 ([**https://www.oracle.com/technetwork/java/javase/downloads/index.html**](https://www.oracle.com/technetwork/java/javase/downloads/index.html))
- Download and extract JMeter `v5.1.1` binaries ([**https://jmeter.apache.org/download_jmeter.cgi**](https://jmeter.apache.org/download_jmeter.cgi))

### **Installation**

For best practices, recomends that you extract the JMeter binaries at root level of your hard drive:

```shell
C:\JMeter\> 
```

### **Post-Installation**

- Download the Plugin Manager jar file ([**https://jmeter-plugins.org**](https://jmeter-plugins.org/))

	The downloaded file must be locate at **`JMETER_HOME\lib\ext`** folder once you extract the JMeter binaries.

- Recommended plugins to install from **`Plugin Manager`**:

  - Custom Thread Groups
  - 3 Basic Graphs
  - Throughput Shaping Timer
  - Dummy Sampler

## **Types of Tests**

There are so many types of `Performance Tests`, like `Smoke Tests`, `Load Tests`, `Stress Tests`, `Spike Tests` and `Endurance Tests`.

**The two ways to generate load**

- Number of users
- Number of Requests

The next step is to decide what kind of performance test your are going to execute:

### **Smoke Test**

Always you are going to execute first a `Smoke Test`, the purpose of this test is to verify if the complete script test is correctly configured.



### **Load Test**

Is a test that is performed at a specific load level. Usually you'll perform load test at many load levels to monitor the behavior of the application.

![LoadTest](images/load-test.png)

### **Stress Test**

Is a test that test the application with loads beyond its normal usage to see up to which point it stays stable and responsive. In a stress test you can add users in steps or constantly over a period of time or you can add a lot of users during that long period of time and see at what point the application stop working.

![StressTest](images/stress-test.png)

### **Spike Test**



### **Endurance Test**



## **Test Plan**

The root element of a test, where its overall settings are specified and all the other elements are contained.

The following window explain the parts of a Test Plan in JMeter:

![JMeter-TestPlan](./images/jm-test-plan.png)

### **Test Plan Structure**

![Structure-Test](./images/structure-test.png)

### **Elements of a Test Plan**

![ComponentsTestScript](images/components-script.png)

#### **Thread Group**

Controls the number of threads (users) JMeter will use to execute a test.

>**NOTE:** A `Thread Group` represent a Test Case.

##### **How to add a Thread Group**

![Add-Thread_group](images/add-thread-group.png)

##### **Properties of a Thread Group**

![PropertiesThreadGroup](images/properties-thread-group.png)

##### **Configuration Elements**

Used to setup default configurations and variables for later use.

These are the **`config elements`** that JMeter manage:

![ConfigElements](images/config-elements.png)

##### **Controllers**

Controllers are the children of **`Thread Grups`** and there are 2 types of controllers:

- **Logic Controllers.** Let you customize the logic to decide when to send requests.

![LogicControllers](images/logic-controllers.png)

- **Samplers.** Perform a request, generating one or more results.

![Samplers](images/samplers.png)

##### **Timer**

Under a **`sampler`** or under a **`Thread Group`**, there are **`Timers`**, that introduce a delay (pause) between requests.

![Timers](images/timers.png)

**Timer Example:**

![TimerExample](images/timer-example.png)

##### **Assertion**

Assertions validate a response is as expected.

![Assertions](images/assertions.png)

#### **Listener**

Listen to responses and aggregate metrics.

![Listeners](images/listeners.png)

### **Execution Order and Rules**

#### **Types of Elements in the Tree Structure**

- **Ordered**
  - Controllers and Samplers
	
	![OrderedElementsExample](images/ordered-elements-example.png)

- **Hierarchical (scoped)**
  - Everything else (config elements, assertions, timers, etc.)

	![HierarchiElementsExample](images/hierarchi-elements-example.png)

#### **Execution Order**

![ExecutionOrder](images/execution-order.png)

>**IMPORTANT:** The last 3 elements do not execute if the server is not responding.

#### **Configuration Elements Rules**

- The **`User Defined Variables`** configuration element is processed at the start of a test, no matter where it is placed.
- A configuration element inside a tree branch has higher precedence than another element of the same type in a outer branch.
  - **`Configuration Default`** elements are merged, Managers are not.

**Example:**

![ConfigurationElementsExample](images/configuration-elements-example.png)

#### **General Rules**

- Elements are rearranged according to the order of execution.
- Outer elements are executed before inner elements of the same type.
- Some elements are executed before or after each sampler in their scope.
  - If there is more than one element of the same type in the scope, all of them will be processed before or after the sampler.

**Example 1:**

![ExecutionOrderSample1](images/execution-order-sample1.png)

**Example 2:**

![ExecutionOrderSample2](images/execution-order-sample2.png)

**Example 3:**

![ExecutionOrderSample3](images/execution-order-sample3.png)

**Example 4:**

![ExecutionOrderSample4](images/execution-order-sample4.png)

### **Test Fragments**

Hold other elements inside for the purpose of reusing.

Controllers that reference `Test Fragments`:

- **Module Controllers.** References test fragments in the same `Test Plan`.
- **Include Controllers.** References test fragments in external JMeter files.

## **Important Application Performance Metrics**

- **Response Time**

	The spend time that an endpoint response.

- **Throughput**

	The number of transactions or KB/Sec.

- **Error Rate**

	Percentage of errors during a test.

These metrics are important to measure the server performance in terms of:

- CPU
- Memory
- Network

# How to record actions in JMeter

There are two ways to record actions in JMeter:

- **Http(s) Test Script Recorder**
- **BlazeMeter Chrome Extension**

## **Http(s) Test Script Recorder**

You need to follow some requirments for this kind of recorder tool:

- You need Mozilla Firefox to use its Proxy Server.
- Configure the `proxy.cert.validity` of the certificate `ApacheJMeterTemporaryRootCA.crt` in the file `JMETER_HOME\bin\jmeter.properties`.
- Install the last certificate in Firefox.
- Configure the Proxy Server in Firefox.

## **BlazeMeter Chrome Extension**

Requirments for this tool:

- Install this extension from ([**https://chrome.google.com/webstore/detail/blazemeter-the-continuous/mbopgmdnpcbohhpnfglgohlbhfongabi?hl=en**](https://chrome.google.com/webstore/detail/blazemeter-the-continuous/mbopgmdnpcbohhpnfglgohlbhfongabi?hl=en))
- Subscribe in `blazemeter.com` to create a `BlazeMeter` user until you successfully install the Chrome Extension.

# **JMeter Distributed Mode**

There are certain limitations to the number of users you can run, with the CPU and RAM configuration for a single machine.

## **JMeter Distributed Mode Architecture**

![DistributedMode](images/distributed-mode.png)

**Resource sites:**

- [**http://blazedemo.com**](http://blazedemo.com)
- [**https://the-internet.herokuapp.com/login**](https://the-internet.herokuapp.com/login)
