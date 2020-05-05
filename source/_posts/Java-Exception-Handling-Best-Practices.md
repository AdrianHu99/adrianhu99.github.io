---
title: Java Exception Handling Best Practices
top: false
cover: false
toc: true
mathjax: true
date: 2020-04-21 06:40:45
summary: Java Exception Handling Best Practices
categories: Tech
tags:
    - Java
password:
---

#### Do **NOT** just catch Exception or Throwable, which will also catch RuntimeException
<!--more-->
  
```
// Bad
try {
  ...
} catch (Throwable th) {
  ...
}
// Good
try {
  ...
} catch (SpecificException ex) {
  ...
}
```
#### When catching an exception, do **NOT** just throw it. Instead, do something like **throw it with some description**, **log an error** or **stop the process.**

**If you catch an exception and do nothing or just log and then let the method continue, include a comment why it's ok to ignore the exception**
```
// Bad
try {
  ...
} catch (SpecificException ex) {
  throw ex;
}
// Good 
try {
  ...
} catch (SpecificException ex) {
  log.error("This function does not work due to SpecificException: ", ex);
}
```

OR

```
try {
  ...
} catch (SpecificException ex) {
  throw new SpecificException("This function does not work due to SpecificException: ", ex);
}
```



OR



```
try {
  ...
} catch (SpecificException ex) {
  // Let the method continue because xyz...
  log.info("xxxxxx");
}
```
  

#### When catching an exception, we may want to log an error or warning, and do **NOT** just log the string without the stacktrace

  
```
// Bad
try {
  ...
} catch (SpecificException ex) {
  log.error("Something wrong...");
}
// Good 
try {
  ...
} catch (SpecificException ex) {
  log.error("This function does not work due to SpecificException: ", ex);
}
```
  

#### How all kinds of different methods in Exception work in the console

  
```
public class TestAllMethods {
	static final Log log = LogFactory.getLog(TestAllMethods.class);
	public static void main(String[] args) {
		try {
			System.out.println(10/0);
		} catch (ArithmeticException ex) {
			ex.printStackTrace();
			//You will get: 
			// java.lang.ArithmeticException: / by zero
			//		at TestAllMethods.main(TestAllMethods.java:10)

			log.error("Try just the exception: \n", ex);
			// You will get: 
			// Sep 06, 2017 3:45:54 PM TestAllMethods main
			// SEVERE: Try just the exception: 

			// java.lang.ArithmeticException: / by zero
			//  	at TestAllMethods.main(TestAllMethods.java:10)


			log.error("Try getMessage(): \n" + ex.getMessage());  
            // You will get:
			//  Sep 06, 2017 3:45:54 PM TestAllMethods main
			//  SEVERE: Try getMessage(): 
			//  / by zero

			log.error("Try toString(): \n" + ex.toString());
			// You will get:
     		// Sep 06, 2017 3:45:54 PM TestAllMethods main
			// SEVERE: Try toString(): 
			// java.lang.ArithmeticException: / by zero


			log.error("Try getStackTrace(): \n" + ex.getStackTrace());
			// You will get:
			// Sep 06, 2017 3:45:54 PM TestAllMethods main
			// SEVERE: Try getStackTrace(): 
			// [Ljava.lang.StackTraceElement;@5a07e868


			log.error("Try Arrays.toString(ex.getStackTrace()): \n" + Arrays.toString(ex.getStackTrace()));
			// You will get:
			// Sep 06, 2017 3:45:54 PM TestAllMethods main
			// SEVERE: Try Arrays.toString(ex.getStackTrace()): 
			// [TestAllMethods.main(TestAllMethods.java:10)]

			log.error("Try getCause(): \n" + ex.getCause());
			// You will get: 
			// Sep 06, 2017 3:45:54 PM TestAllMethods main
			// SEVERE: Try getCause(): 
			// null
		}
	}
}
```
**Conclusions:**

1) **ex.toString()** is better than **ex.getMessage()** as **toString** includes the exception class name, which **getMessage** does not;

2) **ex.getStackTrace()** will return an array of **StackTraceElement**, so do **NOT** print that directly, instead we need **Arrays.toString(ex.getStackTrace())** to show the content of that exception;

3) **ex.getCause()** will show you the cause of this exception or null if the cause is nonexistent or unknown.

  

#### Try to **avoid** duplicated stack trace by **NOT** log an exception with the stack trace and then throw it

  
```
// Bad
public static void main(String[] args) {
	try {
		test();
	} catch (SQLException ex) {
		log.error("second level: ", ex);
	}
}
private static void test() throws SQLException {
	try {
		throw new SQLException();
	} catch (SQLException ex) {
		log.error("first level: ", ex);
		throw new SQLException(ex);
	}
}
// You will get: 
Sep 06, 2017 4:12:40 PM MultipleException test
SEVERE: first level: 
java.sql.SQLException
	at MultipleException.test(MultipleException.java:19)
	at MultipleException.main(MultipleException.java:11)

Sep 06, 2017 4:12:40 PM MultipleException main
SEVERE: second level: 
java.sql.SQLException: java.sql.SQLException
	at MultipleException.test(MultipleException.java:22)
	at MultipleException.main(MultipleException.java:11)
Caused by: java.sql.SQLException
	at MultipleException.test(MultipleException.java:19)
	... 1 more


// Good 
public static void main(String[] args) {
	try {
		test();
	} catch (SQLException ex) {
		log.error("wrong: ", ex);
	}
}
private static void test() throws SQLException {
	try {
		throw new SQLException();
	} catch (SQLException ex) {
		//log.error("first level: ", ex);
		throw new SQLException("first level: ", ex);
	}
}
// You will get: 
Sep 06, 2017 4:16:25 PM MultipleException main
SEVERE: wrong: 
java.sql.SQLException: first level: 
	at MultipleException.test(MultipleException.java:22)
	at MultipleException.main(MultipleException.java:11)
Caused by: java.sql.SQLException
	at MultipleException.test(MultipleException.java:19)
	... 1 more
```
  

  

#### Remember to **release the resource** using try-with-resource or try-catch-finally block

  
```
// Bad
try {
  Connection conn = getConnection();
} catch (SpecificException ex) {
  log.error("This function does not work due to SpecificException: ", ex);
}


// Good 
try {
  Connection conn = getConnection();
  ...
} catch (SpecificException ex) {
  log.error("This function does not work due to SpecificException: ", ex);
} finally {
  context.close(conn);
}
```

OR

```
try (Connection conn = getConnection()) {
  ...
} catch (SpecificException ex) {
  log.error("This function does not work due to SpecificException: ", ex);
} 
```
  

#### If you are using try-with-resource, the implicit finally() block could throw an exception A, and if it happens when something in try block also throws an exception B, A will be suppressed exception of B, and log.warn/error/info() will print both exceptions out.

  
```
Nov 20, 2017 1:17:02 PM toml.main.Main logException
WARNING: logException - MyExceptionA: 
toml.main.MyExceptionA: MyExceptionA in run
    at toml.main.MyAutoClose.run(MyAutoClose.java:7)
    at toml.main.Main.callMyAutoClose(Main.java:25)
    at toml.main.Main.main(Main.java:12)
    Suppressed: toml.main.MyExceptionB: MyExceptionB in close
        at toml.main.MyAutoClose.close(MyAutoClose.java:13)
        at toml.main.Main.callMyAutoClose(Main.java:26)
        ... 1 more
        ```