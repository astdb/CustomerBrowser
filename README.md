Customer Browser
-----------------

This application implements capability for reading and displaying a list of customers and order totals, and individual customer order information from a paginated XML API. The application is built in Go programming language. 

Configuration
-------------

A working Go language installation is required to build and run the application from a machine which has network connectivity to the BigCommerce API endpoints. Instructions to download, install and configure Go for all major operating system platforms are available at https://golang.org/dl/ (for instance, Linux-specific information is available at https://dl.google.com/go/go1.11.linux-amd64.tar.gz). 

Once Go is installed and available at a command line, navigate to the directory where CustomerBrowser.go file is located, and type 'go run CustomerBrowser.go' to run the application (alternatively, you can build a binary by running 'go build CustomerBrowser.go' and then run './CustomerBrowser'). The application will then start and be available at http://localhost:8080/ 

Code Design
-----------

The application uses two main HTTP handler functions to provide the main customer list view and customer-specific view (mainHandler() and customerHandler()). These functions in turn use other functions for getting data from Customer and Orders APIs for display. 

 - main(): defines HTTP handler functions for main and customer views and starts the HTTP server. 
 - mainHandler(): Reads page ID from URL and requests customer data for taht customer API page (API is read in 50-item pages). It stores customer information in a hashmap, gets order detail from orders API, updates the hashmap with order totals for each customer and displays them on a webpage. 
 - customerHandler(): Reads customer ID from URL, gets specific customer object from customers API, gets list of orders for that customer from orders API, and displays order/total value info on a webpage. 
 - APIPageValid(): Takes a page ID and checks if that's a valid page for customers API. It's used by the main view to provide back/forward links on the customer list web page. 
 - GetCustomer(): Takes a customer ID and returns the corresponding customer object from customers API (and an error in case of failure). 
 - GetCustomers(): Takes an integer page number and returns a list of customer objects from that specific page of customers API (and an error in case of failure).
 - GetOrders(): Takes a customer ID. If the customer ID is >0 will return a list of orders filtered by customer, else a full list of orders (inefficient). 


Future Improvements
-------------------

 - The implementation assumes customer and order data can be handled on a single machine.
 - Configuration data needs to be either read from disk files or a database instead of being set in code.
 - Need to use proper HTML templating on front end for safer data rendering.
 - Implement method to read part of order API for each page of customers (e.g. get order total per customer rather than iterating through the full orders list). 
