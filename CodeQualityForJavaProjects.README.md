
# Improving Code Quality for Java Projects


## What is Code Quality & Why it matters?
<pre>
    1.Reliability:
      Should work consistently without frequent crashes.
    2.Consistent Code Style:
      Should follow consistent code style and naming conventions applicable to the language
    3.Maintainable: 
      Should be easy to understand. Maintainable code is easy to extend and add new functionality.
    4.Well-tested: 
      Code that has well-written tests tends to have fewer bugs
    5.Efficient:
      Should not use unnecessary resources to perform the desired operations
    6.Secure:
      Should prevent coding vulnerabilities like SQL injection
    7.Lower Technical Debt: 
      Having low technical debt allows teams to move fast and develop new functionality without being slowed down by low quality and non-maintainable code
  </pre>
## Tools to achieve this.
  ### Checkstyle
    Checkstyle is a static code analysis tool used in software development for checking if Java source code complies with coding rules. The checks performed by Checkstyle are        mainly limited to the presentation of the code. These checks do not confirm the correctness or completeness of the code.
    Using Checkstyle will ensure that a consistent coding style is followed by the team developing the code making it easier to read and understand.
  <pre>
      Below are some of the checks that can be performed using checkstyle:
        1.Naming conventions of attributes and methods
        2.The number of function parameters
        3.Line lengths
        4.The presence of mandatory headers like copyrights
        5.The use of imports, and scope modifiers
        6.The spaces between some characters
        7.The practices of class construction
        8.Multiple code complexity measurements
   </pre>
   ### PMD
    PMD (Programming Mistake Detector) is a static code analyzer that reports on issues found within the application code.
    PMD can help detect issues in the code that could cause issues when the code is shipped to production.
    Possible bugs — Empty try/catch/finally/switch blocks/eating original exception and throwing a new one
    <pre>
        1.Dead code — Unused local variables, parameters, and private methods
        2.Empty if/while statements
        3.Overcomplicated expressions — Unnecessary if statements, for loops that could be while loops
        4.Suboptimal code — Wasteful String/StringBuffer usage
        5.Classes with high Cyclomatic Complexity measurements
        6.Incorrect BigDecimal Usage
    </pre>
   ### Code Coverage Metrics
        Tools like JaCoCo can be used to figure out the code coverage.
    
