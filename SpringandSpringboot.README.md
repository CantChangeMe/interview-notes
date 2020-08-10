

## How to make spring frameworks log level to DEBUG
  
  logging.level.org.springframework = DUBUG

## What steps spring framework follows when you start the application?
<pre>
  1.It does component scan for all the beans annotated with @Component,@Respository,@Service etc.
  2.It creates beans for them.
  3.It creates beans for dependencies also and autowires them and autovires them.
 <pre>
