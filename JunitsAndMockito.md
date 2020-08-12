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

  </pre>
  
        

