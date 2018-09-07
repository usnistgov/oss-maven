
# Build Features

A number of build features are configured by the [oss-parent](oss-parent/) project when [used as
the parent](features.html) of another project. Some features are automatic, while others require use of specific commands.

*   Use of the [Maven Release Plugin](http://maven.apache.org/maven-release/maven-release-plugin/)
    supporting automated releases of project revisions. Use of this feature requires configuration
    of the &lt;scm&gt;/&lt;developerConnection&gt; element in the project POM. A release can be performed using
    the command:
  
    ```console
    mvn -Prelease release:clean release:prepare release:perform
    ```

    The profile "release" triggers building javadoc documentation, which is omitted during the
    regular build process to save build time.

*   Configuration of the site plugin with Markdown support to produce Bootstrap documentation pages like this one. The
    site can be built using the Maven command:
  
    ```console
    mvn -Prelease site site:deploy
    ```

*   [Jacoco](http://www.eclemma.org/jacoco/trunk/doc/maven.html) is used to perform code coverage analysis based on JUnit tests. A site report will be
    produced containing coverage information.

*   Use of the [Maven PMD Plugin](https://maven.apache.org/plugins/maven-pmd-plugin/) to perform
    code analysis. Issues found at [levels 1 and 2]
    (https://pmd.github.io/pmd-5.3.3/customizing/rule-guidelines.html) will fail the build.

*   The [Tag List Maven plugin](http://www.mojohaus.org/taglist-maven-plugin/) is used to generate
    a report of all comments marked "TODO" or "FIXME".

*   The Maven [Checkstyle Plugin](https://maven.apache.org/plugins/maven-checkstyle-plugin/) is
    used to check code for code style issues. The style checked is configured to use the [checkstyle rules](https://github.com/usnistgov/oss-maven/blob/master/build-support/src/main/resources/license/nist/license.txt)
    provided by the [oss-build-support](../oss-build-support/) project.

*   Building of Javadoc documentation will occur if the profile "release" is chosen using:

    ```console
    mvn -Prelease install
    ```

*   The [license Maven Plugin](http://code.mycila.com/license-maven-plugin/) is used to check that
    the appropriate NIST software license is used. All source files are checked to ensure that the [required license content](https://github.com/usnistgov/oss-maven/blob/master/build-support/src/main/resources/license/nist/license.txt),
    provided by the [oss-build-support](../oss-build-support/) project, is included in all java source files.
    The build is failed if a license is missing.
    
    To apply licenses to all source files use:
    
    ```console
    mvn license:format
    ```
    
*   The [Formatter Maven Plugin](https://code.revelc.net/formatter-maven-plugin/) is used to check that
    all Java sources are formatted according the projects formatting policies,
    provided by the [oss-build-support](../oss-build-support/) project.
    The build is failed if source is not properly formatted.
    
    To reformat all source files use:
    
    ```console
    mvn formatter:format
    ```

*   The [Maven enforcer Plugin](http://maven.apache.org/enforcer/maven-enforcer-plugin/) is used to
    check that Java 1.8 or later is used, that the Maven version is 3.0 or higher, and that plugins
    are properly versioned.
    