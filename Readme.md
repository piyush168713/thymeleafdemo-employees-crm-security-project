# <code>Customer Relationship Management Project</code>

[See Dependency Tree](https://github.com/piyush168713/thymeleafdemo-employees-crm-security-project/blob/master/pom.xml)


## <code>Key Features</code>

### CRUD
The CRUD stands for Create, Read/Retrieve, Update, and Delete. These are the four basic functions of the persistence storage.
The CRUD operation can be defined as user interface conventions that allow view, search, and modify information through computer-based forms and reports.


controller/EmployeeController.java
```java
	 @GetMapping("/showFormForAdd")
		public String showFormForAdd(Model theModel) {

			// create model attribute to bind form data
			Employee theEmployee = new Employee();

			theModel.addAttribute("employee", theEmployee);

			return "/employees/employee-form";
		}
	
	
	@PostMapping("/save")
	public String saveEmployee(@ModelAttribute("employee") Employee theEmployee) {
		
		// save the employee
		employeeService.save(theEmployee);
		
		// use a redirect to prevent duplicate submissions
		return "redirect:/employees/list";
	}
```

``` java
	@GetMapping("/list")
	public String listEmployees(Model theModel) {
		
		// get employees from db
		List<Employee> theEmployees = employeeService.findAll();
		
		// add to the spring model
		theModel.addAttribute("employees", theEmployees);
		
		return "/employees/list-employees";
		// Here, the thymeleaf (html) template name must be list-employees. (list-employees.html)
		// i.e. src/main/resources/templates/list-employees.html
	}
```

```java
	@GetMapping("/showFormForUpdate")
	public String showFormForUpdate(@RequestParam("employeeId") int theId,
									Model theModel) {
		
		// get the employee from the service
		Employee theEmployee = employeeService.findById(theId);
		
		// set employee as a model attribute to pre-populate the form
		theModel.addAttribute("employee", theEmployee);
		
		// send over to our form
		return "/employees/employee-form";			
	}
```

```java
	@GetMapping("/delete")
	public String delete(@RequestParam("employeeId") int theId) {
		
		// delete the employee
		employeeService.deleteById(theId);
		
		// redirect to /employees/list
		return "redirect:/employees/list";
		
	}
```




### Sorting

service/EmployeeServiceImpl.java
```java
	@Override
	public List<Employee> findAll() {
		return employeeRepository.findAllByOrderByLastNameAsc();
	}

	@Override
	public List<Employee> searchBy(String theName) {
		
		List<Employee> results = null;
		
		if (theName != null && (theName.trim().length() > 0)) {
			results = employeeRepository.findByFirstNameContainsOrLastNameContainsAllIgnoreCase(theName, theName);
		}
		else {
			results = findAll();
		}
		return results;
	}
```



### Logging Support
### Searching by name
### User Authentication based on roles
<br><br>


