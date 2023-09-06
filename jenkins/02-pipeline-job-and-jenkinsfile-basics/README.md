**Pipeline Job:**

![](.//media/image1.png)

![](.//media/image2.png)

![](.//media/image3.png)
![](.//media/image4.png)

**Jenkinsfile Syntax**

**Execute some logic AFTER all stages executed:**

![](.//media/image5.png)

**Define Conditionals for each stage:**

For example, you want to run test only on dev or master branch

![](.//media/image6.png)

Or, you only want to build the application if there are codechanges

![](.//media/image7.png)

getGitChanges() will be a groovy script that checks if there were any
changes in the code and sets the value of the CODE_CHANGES boolean

**Environment variables:**

See them at <http://jenkins.local:8080/env-vars.html/>

We can define our own environment variables

![](.//media/image8.png)

**Using Credentials in Jenkinsfile:**

1\) Define Credentials in Jenkins UI

2\) credentials("credentials-ID") binds the credentials to our env
variable

3)For that we need "Credentials Binding" Plugin

![](.//media/image9.png)

![](.//media/image10.png)

If we need credentials only in one stage, we can use Wrapper Syntax

![](.//media/image11.png)

**Tools Attribute for Build Tools**

Only 3 Build Tools available with this method: gradle, maven, jdk

![](.//media/image12.png)

![](.//media/image13.png)

**Parameters**

![](.//media/image14.png)

![](.//media/image15.png)![](.//media/image16.png)![](.//media/image17.png)

**Using external Groovy scripts**

All environmental variables in Jenkinsfile are available in the groovy
script

![](.//media/image18.png)

![](.//media/image19.png)

We can test changes without pushing to git repository by accessing
Replay Section of a build

![](.//media/image20.png)

**Input Parameters for User Input**

![](.//media/image21.png)

![](.//media/image22.png)

![](.//media/image23.png)

**Multi-choice**

![](.//media/image24.png)
