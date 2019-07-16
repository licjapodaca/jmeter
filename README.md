# **Apache - JMeter**
Repository to practice the using of JMeter, an opensource project for many different of tests, like Stress, Performance and Load tests.

- [**Apache - JMeter**](#Apache---JMeter)
- [**Curso de JMeter**](#Curso-de-JMeter)
	- [**Instalacion de JMeter**](#Instalacion-de-JMeter)
		- [**Pre-requisitos**](#Pre-requisitos)
		- [**Instalacion**](#Instalacion)
		- [**Post-Instalacion**](#Post-Instalacion)
	- [**Tipos de Prueba**](#Tipos-de-Prueba)
		- [**Smoke Test**](#Smoke-Test)
		- [**Load Test**](#Load-Test)
		- [**Stress Test**](#Stress-Test)
		- [**Spike Test**](#Spike-Test)
		- [**Endurance Test**](#Endurance-Test)
	- [**Test Plan**](#Test-Plan)
		- [**Test Plan Structure**](#Test-Plan-Structure)
		- [**Elements of a Test Plan**](#Elements-of-a-Test-Plan)
			- [**Thread Group**](#Thread-Group)
				- [**How to add a Thread Group**](#How-to-add-a-Thread-Group)
				- [**Properties of a Thread Group**](#Properties-of-a-Thread-Group)
				- [**Configuration Elements**](#Configuration-Elements)
				- [**Controllers**](#Controllers)
				- [**Timer**](#Timer)
				- [**Assertion**](#Assertion)
			- [**Listener**](#Listener)
		- [**Execution Order and Rules**](#Execution-Order-and-Rules)
			- [**Types of Elements in the Tree Structure**](#Types-of-Elements-in-the-Tree-Structure)
			- [**Execution Order**](#Execution-Order)
			- [**Configuration Elements Rules**](#Configuration-Elements-Rules)
			- [**General Rules**](#General-Rules)
		- [**Test Fragments**](#Test-Fragments)
	- [**Important Application Performance Metrics**](#Important-Application-Performance-Metrics)

# **Curso de JMeter**

## **Instalacion de JMeter**

### **Pre-requisitos**

### **Instalacion**

### **Post-Instalacion**

You must modify the variable called `proxy.cert.validity` from the file called `jmeter.properties` located at the JMETER home directory inside the `bin` folder, specify the amount of time in days of the JMETER certificate expiracy.

Then, from a Http(s) Script Recorder generate the certificate that you need to install in Mozilla Firefox to record HTTPS websits.

## **Tipos de Prueba**

There are so many types of Stress and Performance tests, like Smoke Tests, Load Tests, Stress Tests, Spike Tests and Endurance Tests.

### **Smoke Test**



### **Load Test**



### **Stress Test**



### **Spike Test**



### **Endurance Test**



## **Test Plan**

The root element of a test, where its overall settings are specified and all the other elements are contained.

The following window explain the parts of a Test Plan in JMeter:

![JMeter-TestPlan](./images/jm-test-plan.png =700x)

### **Test Plan Structure**

![Structure-Test](./images/structure-test.png =260x)

### **Elements of a Test Plan**

![ComponentsTestScript](images/components-script.png =500x)

#### **Thread Group**

Controls the number of threads (users) JMeter will use to execute a test.

>**NOTE:** A `Thread Group` represent a Test Case.

##### **How to add a Thread Group**

![Add-Thread_group](images/add-thread-group.png =700x)

##### **Properties of a Thread Group**

![PropertiesThreadGroup](images/properties-thread-group.png =700x)

##### **Configuration Elements**

Used to setup default configurations and variables for later use.

These are the **`config elements`** that JMeter manage:

![ConfigElements](images/config-elements.png =700x)

##### **Controllers**

Controllers are the children of **`Thread Grups`** and there are 2 types of controllers:

- **Logic Controllers.** Let you customize the logic to decide when to send requests.

![LogicControllers](images/logic-controllers.png =700x)

- **Samplers.** Perform a request, generating one or more results.

![Samplers](images/samplers.png =700x)

##### **Timer**

Under a **`sampler`** or under a **`Thread Group`**, there are **`Timers`**, that introduce a delay (pause) between requests.

![Timers](images/timers.png =700x)

**Timer Example:**

![TimerExample](images/timer-example.png =700x)

##### **Assertion**

Assertions validate a response is as expected.

![Assertions](images/assertions.png =700x)

#### **Listener**

Listen to responses and aggregate metrics.

![Listeners](images/listeners.png =700x)

### **Execution Order and Rules**

#### **Types of Elements in the Tree Structure**

- **Ordered**
  - Controllers and Samplers
	
	![OrderedElementsExample](images/ordered-elements-example.png =500x)

- **Hierarchical (scoped)**
  - Everything else (config elements, assertions, timers, etc.)

	![HierarchiElementsExample](images/hierarchi-elements-example.png =500x)

#### **Execution Order**

![ExecutionOrder](images/execution-order.png =350x)

>**IMPORTANT:** The last 3 elements do not execute if the server is not responding.

#### **Configuration Elements Rules**

- The **`User Defined Variables`** configuration element is processed at the start of a test, no matter where it is placed.
- A configuration element inside a tree branch has higher precedence than another element of the same type in a outer branch.
  - **`Configuration Default`** elements are merged, Managers are not.

**Example:**

![ConfigurationElementsExample](images/configuration-elements-example.png =700x)

#### **General Rules**

- Elements are rearranged according to the order of execution.
- Outer elements are executed before inner elements of the same type.
- Some elements are executed before or after each sampler in their scope.
  - If there is more than one element of the same type in the scope, all of them will be processed before or after the sampler.

**Example 1:**

![ExecutionOrderSample1](images/execution-order-sample1.png =600x)

**Example 2:**

![ExecutionOrderSample2](images/execution-order-sample2.png =600x)

**Example 3:**

![ExecutionOrderSample3](images/execution-order-sample3.png =600x)

**Example 4:**

![ExecutionOrderSample4](images/execution-order-sample4.png =600x)

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

