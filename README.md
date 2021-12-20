# log4j-maven-check-action

## TL;DR
Checks if a [vulnerable Log4j 2 Version < 2.16](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-44228) is contained in the dependencies of a Maven based project.

## Dependabot does not check transitive dependencies
At the time of writing, Dependabot does not check transitive dependencies (see https://github.com/dependabot/dependabot-core/issues/2640). The problem is, that you grab hell a lot of software via transitive dependencies, and this was the problem of the [Log4j 2 issue](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-44228). It is recommended, that you check your dependencies with `mvn dependency:list -Dincludes=org.apache.logging.log4j`. Even if it is clean at the time you check this, with the next update or by adding a new depencency, you might catch it. 

So in order to regurlarly check projects, I wrote this stupid simple action that checks for vulnerable log4j 2 versions (< 2.16) and exits the build with an error in case of a finding. Simple but effective. I ain't no script guy, so there will be better ways to do that, feedback welcome ;-)

# Usage

<!-- start usage -->
```yaml
- uses: ralfstuckert/log4u-maven-check-action@v0.0.3
  with:
    # The root of the project where the pom.xml is located.
    #
    # Default is '.'
    project-root: ''
    
    # The (optional) path of the settings xml file
    #
    settings-path: ''
    
    # Personal access token (PAT) that will be passed as environment variable GTIHUB_TOKEN to the maven call.
    #
    # Default: ${{ github.token }}
    token: ''
```
