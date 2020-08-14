## 1.A Guide to Spring Boot RestTemplate
  Difference microservices talk to each other using REST API calls.
  
#### RestTemplate GET Resource
   ###### Plain JSON
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
   ###### POJO Instead of JSON
        private void callGetToDoWithPOJO() {
          **
          **
          ResponseEntity<ToDo> result = restTemplate.exchange(uri, HttpMethod.GET, entity, ToDo.class);
          **
          **
        }
#### RestTemplate POST Resource
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
          
#### RestTemplate PUT Resource
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

#### RestTemplate DELETE Resource
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
          
#### Other Methods for REST calls:
    1.The getForObject() method allows you to directly return the underlying object without the ResponseEntity wrapping.
        ToDo toDo = restTemplate.getForObject(uri, ToDo.class);
        
    2.This method returns a ResponseEntity object with the underlying resource object.
        ResponseEntity result = restTemplate.getForEntity(uri, ToDo.class);
        
        Response:
            <200,ToDo{userId=1, id=1, title='delectus aut autem', completed=false},[Date:"Sat, 18 Jan 2020 04:09:25 GMT"
            
        
## How to submit form data for a post request.
   #### Next, let's look at how to submit a form using the POST method.
      1.we need to set the “Content-Type” header to application/x-www-form-urlencoded.
      This makes sure that a large query string can be sent to the server, containing name/value pairs separated by ‘&‘:
      
        HttpHeaders headers = new HttpHeaders();
        headers.setContentType(MediaType.APPLICATION_FORM_URLENCODED);

      2.We can wrap the form variables into a LinkedMultiValueMap:
        MultiValueMap<String, String> map= new LinkedMultiValueMap<>();
        map.add("id", "1");
      3.We build the Request using an HttpEntity instance:
        ttpEntity<MultiValueMap<String, String>> request = new HttpEntity<>(map, headers);
      4.Finally, we can connect to the REST service by calling restTemplate.postForEntity() on the Endpoint: /foos/form
        
        ResponseEntity<String> response = restTemplate.postForEntity(
        fooResourceUrl+"/form", request , String.class);
 
        assertThat(response.getStatusCode(), is(HttpStatus.CREATED));

## Use OPTIONS to Get Allowed Operations

        Set<HttpMethod> optionsForAllow = restTemplate.optionsForAllow(fooResourceUrl);
        HttpMethod[] supportedMethods
          = {HttpMethod.GET, HttpMethod.POST, HttpMethod.PUT, HttpMethod.DELETE};
        assertTrue(optionsForAllow.containsAll(Arrays.asList(supportedMethods)));

      
