


## Set up a java programming environment in a container: 
This exercise creates a simple java program within a container.

1. Create the container:
`docker run -it --rm --name javahi openjdk:11 bash`
This will create the container and get you into the container using bash

2. Add the nano text editor inside the container
`apt-get update`
`apt-get install vim nano`

3. Create a java doc for editing by entering the following command,
`nano hello.java`
After executing, you should be within the document in the nano editor
Of mention, GNU nano is a user-friendly command line text editor for Unix and Linux operating systems. It includes all the basic functionality of a text editor, such as “text content create/update, search and replace with regular expression support, spell checking, and more.

4. Within the editor, include the following code:
``` java
import java.io.*;
public class Hello {
    public static void main(String[] args){
        System.out.println("hello, world");
    }
}
```
Once complete, exit the doc, safe the file, and confirm the file name. Also, confirm content by entering `cat hello.java`.

5. Java programs require compiling, unlike Python programs. In order to compile the java program, enter `javac hello.java`. This will create a java class, Hello.class. 

6. To test the java program, enter `java Hello`, which should return, `hello, world`

