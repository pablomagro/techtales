---
title: ServletContextListener
tags:
  - ServletContextListener
  - Java
  - Filter
categories:
  - Java
date: 2016-09-13 16:52:53
---


Implementations of this interface recieve notifications about changes to the servlet context of the web application they are part of. To recieve notification events, the implementation class must be configured in the deployment descriptor for the web application.

    public interface ServletContextListener extends EventListener
[Interface][1] for receiving notification events about ServletContext lifecycle changes.

### Methods Summary
##### void contextDestroyed(ServletContextEvent sce)
    Notification that the servlet context is about to be shut down.
All servlets and filters will have been destroyed before any ServletContextListeners  are notified of context destruction.

#### void contextInitialized(ServletContextEvent sce)
    Notification that the web application is ready to process requests.
All ServletContextListeners are notified of context initialization before any filters or servlets in the web application are initialized.

### Set the deployment descriptor.

#### web.xml (Servlet < 3.0)
    Sample web.xml file:

    <?xml version="1.0" encoding="UTF-8"?>
    <web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://java.sun.com/xml/ns/javaee" xmlns:web="http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd" xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd" id="WebApp_ID" version="2.5">
      ...
      <listener>
        <listener-class>example.ExampleApplicationLifeCycleListener</listener-class>
      </listener>
      ...
    </web-app>

####  @WebListener (Servlet >= 3.0)
The `WebListener` annotation is used to register the following types of listeners

* _Context Listener_ (javax.servlet.ServletContextListener)
* _Context Attribute Listener_ (javax.servlet.ServletContextAttributeListener)
* _Servlet Request Listener_ (javax.servlet.ServletRequestListener)
* _Servlet Request Attribute Listener_ (javax.servlet.ServletRequestAttributeListener)
* _Http Session Listener_ (javax.servlet.http.HttpSessionListener)
* _Http Session Attribute Listener_ (javax.servlet.http.HttpSessionAttributeListener)

### Example
Registering ServletContextListeners, which run your code before the web application is started. It waits for specified event happened, then "hijack" the event and run its own event.

__Problem__
You want to initialize a database connection pool before the web application is started, is there a "main()" method in the web application environment?

__Solution__
The ServletContextListener is what you want, it will run your code before the web application is started.

~~~java
package example;

import javax.servlet.annotation.WebListener;
import javax.servlet.ServletContextListener;

@WebListener
public class ExampleApplicationLifeCycleListener implements ServletContextListener {
  public void contextInitialized(ServletContextEvent event) {
    //do on application init
    EntityManagerFactory emf =
            Persistence.createEntityManagerFactory("$objectdb/db/example.odb");
    event.getServletContext().setAttribute("emf", emf);
    System.out.println("ServletContextListener started");
  }

  public void contextDestroyed(ServletContextEvent event) {
    //do on application destroy
    EntityManagerFactory emf =
            (EntityManagerFactory)event.getServletContext().getAttribute("emf");
    emf.close();  
    System.out.println("ServletContextListener destroyed");
  }
}
~~~

### References
1. https://www.ntu.edu.sg/home/ehchua/programming/java/JavaServlets.html
2. https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api/3.1.0
3. http://blog.caucho.com/2009/10/06/servlet-30-tutorial-weblistener-webservlet-webfilter-and-webinitparam/
4. https://www.mkyong.com/servlet/what-is-listener-servletcontextlistener-example/

[1]: http://docs.oracle.com/javaee/7/api/javax/servlet/ServletContextListener.html
