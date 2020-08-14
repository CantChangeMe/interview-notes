# A Guide to Spring Boot RestTemplate
  Difference microservices talk to each other using REST API calls.
  
## RestTemplate GET Resource
   #### Plain JSON
       private void callGetToDoWithString() {

          RestTemplate restTemplate = new RestTemplate();
          String uri = "https://jsonplaceholder.typicode.com/todos/1";

          HttpHeaders headers = new HttpHeaders();
          headers.setAccept(Arrays.asList(MediaType.APPLICATION_JSON));
          HttpEntity<String> entity = new HttpEntity<String>("parameters", headers);

          ResponseEntity<String> result = restTemplate.exchange(uri, HttpMethod.GET, entity, String.class);
          System.out.println(result);
       }
       
       Response:
           <200,{
                "userId": 1,
                "id": 1,
                "title": "delectus aut autem",
                "completed": false
              },[Date:"Sat, 18 Jan 2020 03:39:33 GMT"
   #### POJO Instead of JSON
        private void callGetToDoWithPOJO() {
          **
          **
          ResponseEntity<ToDo> result = restTemplate.exchange(uri, HttpMethod.GET, entity, ToDo.class);
          **
          **
        }
## RestTemplate POST Resource
        	private void callPostToDo() {
              RestTemplate restTemplate = new RestTemplate();

              String uri = "https://jsonplaceholder.typicode.com/todos";

              ToDo newTodo = new ToDo();
              newTodo.setUserId(1);
              newTodo.setTitle("Test Todo");
              newTodo.setCompleted(false);

              HttpHeaders headers = new HttpHeaders();
              headers.setAccept(Arrays.asList(MediaType.APPLICATION_JSON));
              HttpEntity<ToDo> entity = new HttpEntity<ToDo>(newTodo, headers);

              ResponseEntity<ToDo> result = restTemplate.exchange(uri, HttpMethod.POST, entity, ToDo.class);

              System.out.println(result);
          }
          
          Response:
          <201,ToDo{userId=1, id=201, title='Test Todo', completed=false},[Date:"Sat, 18 Jan 2020 03:39:34 GMT"
          
           HTTP Status Code of 201 (CREATED).
          
## RestTemplate PUT Resource
        private void callPutToDo() {
          RestTemplate restTemplate = new RestTemplate();

          String uri = "https://jsonplaceholder.typicode.com/todos/1";

          ToDo newTodo = new ToDo();
          newTodo.setUserId(1);
          newTodo.setId(1);
          newTodo.setTitle("Updated ToDo");
          newTodo.setCompleted(false);

          HttpHeaders headers = new HttpHeaders();
          headers.setAccept(Arrays.asList(MediaType.APPLICATION_JSON));
          HttpEntity<ToDo> entity = new HttpEntity<ToDo>(newTodo, headers);

          ResponseEntity<ToDo> result = restTemplate.exchange(uri, HttpMethod.PUT, entity, ToDo.class);
          System.out.println(result);
         }
         
         Response :
           <200,ToDo{userId=1, id=1, title='Updated ToDo', completed=false},[Date:"Sat, 18 Jan 2020 03:39:34 GMT"

## RestTemplate DELETE Resource
        private void callDeleteToDo() {

            RestTemplate restTemplate = new RestTemplate();

            String uri = "https://jsonplaceholder.typicode.com/todos/1";

            HttpHeaders headers = new HttpHeaders();
            headers.setAccept(Arrays.asList(MediaType.APPLICATION_JSON));
            HttpEntity<String> entity = new HttpEntity<String>("parameters", headers);

            ResponseEntity<String> result = restTemplate.exchange(uri, HttpMethod.DELETE, entity, String.class);
            System.out.println(result);

        }
        
        Response:
          <200,{},[Date:"Sat, 18 Jan 2020 03:39:35 GMT", Content-Type:"application/json; charset=utf-8"
          
## Other Methods for REST calls:
    1.The getForObject() method allows you to directly return the underlying object without the ResponseEntity wrapping.
        ToDo toDo = restTemplate.getForObject(uri, ToDo.class);
        
    2.This method returns a ResponseEntity object with the underlying resource object.
        ResponseEntity result = restTemplate.getForEntity(uri, ToDo.class);
        
        Response:
            <200,ToDo{userId=1, id=1, title='delectus aut autem', completed=false},[Date:"Sat, 18 Jan 2020 04:09:25 GMT"
            
        
