# <h1 align="center">Todo App</h1>


---

<p align="left">

## Overview

The Todo App is a simple Spring Boot application that allows you to maintain list of tasks that you have to do along with the status.

## Technologies Used

- **Framework:** Spring Boot
- **Language:** Java
- **Build Tool:** Maven

## Data Flow

The Todo application follows a structured data flow pattern to handle requests and manage data efficiently:
### Controller

The Controller layer is responsible for handling incoming HTTP requests and delegating them to the appropriate method. It defines API endpoints for various operations, including adding Todo, retrieving Todo, and updating Todo. Each endpoint has a method to ensure proper request handling and response generation.
```java
@RestController
public class TodoController {

    @Autowired
    List<Todo> todoList;
```
The @PostMapping annotation is used for the add/Todo endpoint to handle HTTP POST requests with a JSON request body containing a Todo object. 
```java
 @PostMapping("todo")
    public String addTodo(@RequestBody Todo myTodo)
    {
        todoList.add(myTodo);
        return "todo added";
    }
```

The @GetMapping annotation is used for the todos endpoints to handle HTTP GET requests without a path variable.
```java
@GetMapping("todos")
    public List<Todo> getAllTodos()
    {
        return  todoList;
    }
```
The @PutMapping annotation is used for todo/id/{id}/status endpoint to handel HTTP UPDATE requests with a path variable for Todo Id.
```java
@PutMapping("todo/id/{id}/status")
    public String setTodoStatusById(@PathVariable Integer id,@RequestParam boolean flag)
    {
        for(Todo todo : todoList)
        {
            if(todo.getTodoId().equals(id))
            {
                todo.setTodoStatus(flag);
                return "todo: "   + id  + "updated to " +  flag;
            }
        }

        return "Invalid id";
    }
```
The @DeleteMapping annotation is used for the todo/id/{id} endpoint to handle HTTP DELETE requests with a path variable for the Todo ID.
```java
 @DeleteMapping("todo/id/{id}")
    public String removeTodoById(@PathVariable Integer id)
    {
        for(Todo todo : todoList)
        {
            if(todo.getTodoId().equals(id))
            {
                todoList.remove(todo);
                return "todo: "   + id  + " removed";
            }
        }

        return "Invalid id";
    }

```
## Database Design

The Todo App application utilizes a simple in-memory data structure to store Todo. In a production environment, it is advisable to replace this in-memory storage with a relational or NoSQL database for better data persistence and scalability.

### In-Memory Data Structure

The primary data structure used in this application is a `List` of `Todo` objects. Each `Todo` object represents a todoId, todoName and todoStatus. This structure allows for easy manipulation of Todo but is not suitable for long-term data storage.

```java
public class Todo {

    private Integer todoId;
    private String todoName;
    private boolean todoStatus;
```

## Data Structures Used

### List

The application utilizes the Java `List` data structure to maintain a collection of `Todo` objects. This dynamic data structure allows for the storage and retrieval of Todo. However, please note that this implementation is limited to in-memory storage and is not suitable for persisting data in a production environment.

```java
 @Bean
    public List<Todo> getDataSource()
    {
        return new ArrayList<>();
    }
```

### Todo Class

The `Todo` class defines the structure for storing todo information. It includes three fields: `todoId` (to identify the todo), `todoName` (name of the task) and `todoStatus` (status of todo). Instances of this class are used to represent todo and manage todo.

```java
public class Todo {

    private Integer todoId;
    private String todoName;
    private boolean todoStatus;
```

## Usage

1. Use a tool like [Postman](https://www.postman.com/) to make HTTP requests to the provided endpoints.

2. Create Todo using the "Add a New Todo" endpoint with a POST request.

3. Retrieve Todo, manage Todo and delete Todo using the provided endpoints.

## Project Structure

The project follows a standard Spring Boot application structure with components organized into layers:

- **Controller:** Handles incoming HTTP requests and defines API endpoints.
- **BeanManager:** Contains Spring bean configurations.

## Data Storage

Todo are stored in-memory using a `List`. In a production environment, you should consider using a database for data persistence.

<!-- Acknowledgments -->
## Acknowledgments
Thank you to the Spring Boot and Java communities for providing excellent tools and resources.

<!-- Contact -->
## Contact
For questions or feedback, please contact [Ravindra Suthar](mailto:ravindrasuthar201@gmail.com).

