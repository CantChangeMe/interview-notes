

## How to make spring frameworks log level to DEBUG
  
  logging.level.org.springframework = DUBUG

## What steps spring framework follows when you start the application?
<pre>
  1.It does component scan for all the beans annotated with @Component,@Respository,@Service etc.
  2.It creates beans for them.
  3.It creates beans for dependencies also and autowires them and autovires them.
 <pre>

## Setter or Constructor injection
  For injecting mandatory dependencies we use constrcutor injection.For optional dependencies we can use setter injection.
  
## Do we really need to use @Autowired for setter or constructor? Or even do we need setter or constructor.
    No .We dont need @Autowired annotation on setters or contructor.We dont even need setter or constructor.
    Just use member variable with @Autowired annotaion.
  
