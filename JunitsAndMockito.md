# Unit testing using Junits And Mockito
<pre>
JUinit4:

   assertEquals(expected, actual);
   
   @Test annotation on method
   
   test method should be public and void
   
   If there are no conditions in test method then it will always pass.No failure = success
   
   you can replace assertEquals(false,obj.isValidScenario()); to assertFalse(obj.isValidScenario());
      assertEquals(false,obj.isValidScenario());
      assertFalse(obj.isValidScenario());
      
  assertTrue(obj.isValidScenario());
  
  @Before , @After // They run before and after every test method respectively.
  
  @BeforeClasss, @AfterClass // They run before any of tests is run and after all tests have been run respectvely
  
  int [] expected = new int[]{3,4,5,12};
  int [] actual = new int[]{12,5,4,3};
    assertArrayEquals(expected, actual);
    
  Handling exception
  @Test
  public void testException(){
    int [] actual = null;
    assertThrows(NullPointerException.class,() -> Arrays.sort(actual));
    
  }  
  
  Run parameterized test
   Steps:
      1.@Runwith(Parameterized.class) at class level
      2.Contructor with input output
      3.@Parameter annotated method that returns Collection<String []>

  
   Create suites:
      @RunWith(Suite.class)
      @SuiteClasses({ArraysTest.class,StringHelperTest.class})

 
  
  Testing a class with a dependency:
      --By creating stub class.//Stub class is dummy class which fakes real class
         
         @Test
         public void getSpringRelatedToDos(){
             ToDoService toDoServiceStub = new ToDoServiceStub();
             ToDoBusinessImpl toDoBusiness = new ToDoBusinessImpl(toDoServiceStub);
             Assertions.assertEquals(2, toDoBusiness.getToDosRelatedToSpring("Dummy").size());
         }
         
      --By Mocking the class or interface using Mockito framework
        
        @Test
        public void getSpringRelatedToDosWithMockito(){
            ToDoService toDoServiceMock = mock(ToDoService.class);
            when(toDoServiceMock.getToDoList("Dummy")).thenReturn(List.of("Spring is awesome","Welcome to Spring boot","Dance lessons"));
            ToDoBusinessImpl toDoBusiness = new ToDoBusinessImpl(toDoServiceMock);
            Assertions.assertEquals(2, toDoBusiness.getToDosRelatedToSpring("Dummy").size());
        }
        
      Stubbing variations with Mockito
             @Test
    public void stubMethodWithOneArg(){
        List<Integer> mockList = mock(List.class);
        when(mockList.size()).thenReturn(2);
        assertEquals(2,mockList.size());

    }

    @Test
    public void stubMethodWithTwoCalls(){
        List<Integer> mockList = mock(List.class);
        when(mockList.size()).thenReturn(2).thenReturn(4);
        assertEquals(2,mockList.size());
        assertEquals(4, mockList.size());

    }

    @Test
    public void stubMethodWithMatchers(){
        List<String> mockList = mock(List.class);
        when(mockList.get(anyInt())).thenReturn("Hi");
        assertEquals("Hi",mockList.get(0));
        assertEquals("Hi",mockList.get(1));
    }

    @Test
    public void stubMethodWithException(){
        List<String> mockList = mock(List.class);
        when(mockList.get(1)).thenThrow(new RuntimeException("Hi"));
        Exception exception =  assertThrows(RuntimeException.class,() -> mockList.get(1));

        assertEquals("Hi",exception.getMessage());
    }
    
    BBD style testing
       Jusy a good way of oganizing a test in the form of
       Given //Setup part
       When  //Actual invocation
       Then  //assertThat part
       
          //import static org.mockito.BDDMockito.given;
          //import static org.hamcrest.CoreMatchers.is;
          //import static org.junit.Assert.assertThat;
          
          @Test
          public void getSpringRelatedToDosWithMockitoUsingBDD(){
              //Given
              ToDoService toDoServiceMock = mock(ToDoService.class);
              given(toDoServiceMock.getToDoList("Dummy")).willReturn(List.of("Spring is awesome","Welcome to Spring boot","Dance lessons"));
              ToDoBusinessImpl toDoBusiness = new ToDoBusinessImpl(toDoServiceMock);
              //When
              int size = toDoBusiness.getToDosRelatedToSpring("Dummy").size();
              //Then
             assertThat (size, is(2));
          }
          
      Verify calls on mock
         if a particular method was called in case we are testing a void method.
         We want to test how many time a particular method was called inside that void method.
             @Test
             public void deleteToDosNotRelatedToSpringUsingBDD(){
                 //Given
                 ToDoService toDoServiceMock = mock(ToDoService.class);
                 given(toDoServiceMock.getToDoList("Dummy")).willReturn(List.of("Spring is awesome","Welcome to Spring boot","Dance lessons"));
                 ToDoBusinessImpl toDoBusiness = new ToDoBusinessImpl(toDoServiceMock);
                 //When
                 toDoBusiness.deleteToDosNotRelatedToSpring("Dummy");
                 //Then
                 verify(toDoServiceMock ,times(1)).deleteToDo("Dance lessons");//verfiry is non BDD style
                 then(toDoServiceMock).should().deleteToDo("Dance lessons");// BDD style
                 then(toDoServiceMock).should(never()).deleteToDo("Spring is awesome");// BDD style
             }

             @Test
             public void deleteToDosNotRelatedToSpringUsingBDD_Atleast(){
                 //Given
                 ToDoService toDoServiceMock = mock(ToDoService.class);
                 given(toDoServiceMock.getToDoList("Dummy")).willReturn(List.of("Spring is awesome","Welcome to Spring boot","Dance lessons"));
                 ToDoBusinessImpl toDoBusiness = new ToDoBusinessImpl(toDoServiceMock);
                 //When
                 toDoBusiness.deleteToDosNotRelatedToSpring("Dummy");
                 //Then
                 verify(toDoServiceMock ,atLeast(1)).deleteToDo("Dance lessons");
             }
         
         Argument capturing:
                @Test
                public void deleteToDosNotRelatedToSpringUsingBDD_ArgumentCapture(){
                    //Given
                    ArgumentCaptor<String> stringArgumentCaptor = ArgumentCaptor.forClass(String.class);
                    ToDoService toDoServiceMock = mock(ToDoService.class);
                    given(toDoServiceMock.getToDoList("Dummy")).willReturn(List.of("React is also awesome","Welcome to Spring boot","Dance lessons"));
                    ToDoBusinessImpl toDoBusiness = new ToDoBusinessImpl(toDoServiceMock);
                    //When
                    toDoBusiness.deleteToDosNotRelatedToSpring("Dummy");
                    //Then
                    then(toDoServiceMock).should(times(2)).deleteToDo(stringArgumentCaptor.capture());//BDD style
                   // assertThat(stringArgumentCaptor.getValue(), is("Dance lessons"));
                    assertThat(stringArgumentCaptor.getAllValues().size(), is(2));
                }
         
         Using @Mocks , @InjectMocks
            //@SpringBootTest
            @Runwith(MockitoJUnitRunner.class)
            class ToDoBusinessImplMockitoInjectTest {

                @Mock
                ToDoService toDoService;

                @InjectMocks
                ToDoBusinessImpl toDoBusiness;

                @Test
                public void getSpringRelatedToDosWithMockito(){
                    when(toDoService.getToDoList("Dummy")).thenReturn(List.of("Spring is awesome","Welcome to Spring boot","Dance lessons"));
                    assertEquals(2, toDoBusiness.getToDosRelatedToSpring("Dummy").size());
                }
         }
         
         @Rule annotation
            Its better to use @Rule because you can define multiple rules whereas in case of @Runwith(SomeRunner.class)//@Runwith(MockitoJUnitRunner.class). you 
            can have only one runner.
         
         Using spy 
            Used to spy on a class.Like mocking a desired method call on the class and letting other methods of class as it is.
            
            
</pre>  
 
  ## Static imports
  <pre>
           Static imports are used to save your time and typing. If you hate to type same thing again and again then you may find such imports interesting.
               1.The import allows the java programmer to access classes of a package without package qualification.
               2.The static import feature allows to access the static members of a class without the class qualification.
  </pre>
        

