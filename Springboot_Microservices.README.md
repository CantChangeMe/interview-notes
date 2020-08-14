# A Guide to Spring Boot RestTemplate
  Difference microservices talk to each other using REST API calls.
  
## RestTemplate GET Resource
       private void callGetToDoWithString() {

          RestTemplate restTemplate = new RestTemplate();
          String uri = "https://jsonplaceholder.typicode.com/todos/1";

          HttpHeaders headers = new HttpHeaders();
          headers.setAccept(Arrays.asList(MediaType.APPLICATION_JSON));
          HttpEntity<String> entity = new HttpEntity<String>("parameters", headers);

         ```diff
        + ResponseEntity<String> result = restTemplate.exchange(uri, HttpMethod.GET, entity, String.class);
         ```
          System.out.println(result);
       }
       
       Response:
           <200,{
                "userId": 1,
                "id": 1,
                "title": "delectus aut autem",
                "completed": false
              },[Date:"Sat, 18 Jan 2020 03:39:33 GMT"

