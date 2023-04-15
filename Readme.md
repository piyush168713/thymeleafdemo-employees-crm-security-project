# <code>Customer Relationship Management Project</code>

[See Dependency Tree](https://github.com/piyush168713/thymeleafdemo-employees-crm-security-project/blob/master/pom.xml)


## <code>Key Features</code>

### CRUD

### Sorting
### Logging Support
### Searching by name
### User Authentication based on roles
<br><br>

```java
 @GetMapping("/showFormForAdd")
	public String showFormForAdd(Model theModel) {
		
		// create model attribute to bind form data
		Employee theEmployee = new Employee();
		
		theModel.addAttribute("employee", theEmployee);
		
		return "/employees/employee-form";
	}
```
