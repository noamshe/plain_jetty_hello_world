Thanks to:
https://wiki.eclipse.org/Jetty/Tutorial/Jetty_HelloWorld

this tutorial shows how you can develop code against the Jetty API with the jetty classes on your class path. If you want to use Maven or standard web applications, see the Jetty and Maven HelloWorld tutorial.

Details

Downloading the Jars
Jetty is decomposed into many jars and dependencies to achieve a minimal footprint by selecting the minimal set of jars. Typically it is best to use something like Maven to manage jars (see Jetty and Maven HelloWorld Tutorial), but for this tutorial, we will use an aggregate jar that contains all of the jetty classes in one jar.

You can manually download the jetty aggregate-all jar and the servlet api jar using wget or similar command (for example, curl) or a browser. Use wget as follows:

mkdir Demo
cd Demo
JETTY_VERSION=7.0.2.v20100331
wget -U none http://repo1.maven.org/maven2/org/eclipse/jetty/aggregate/jetty-all/$JETTY_VERSION/jetty-all-$JETTY_VERSION.jar
wget -U none http://repo1.maven.org/maven2/javax/servlet/servlet-api/2.5/servlet-api-2.5.jar
Writing a HelloWorld Example
The Embedding Jetty tutorial contains many examples of writing against the Jetty API. For this tutorial, we will use a simple HelloWorld handler with a main method to run the server. In an editor, edit the file HelloWorld.java and add the following content:

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.ServletException;
 
import java.io.IOException;
 
import org.eclipse.jetty.server.Server;
import org.eclipse.jetty.server.Request;
import org.eclipse.jetty.server.handler.AbstractHandler;
 
public class HelloWorld extends AbstractHandler
{
    public void handle(String target,
                       Request baseRequest,
                       HttpServletRequest request,
                       HttpServletResponse response) 
        throws IOException, ServletException
    {
        response.setContentType("text/html;charset=utf-8");
        response.setStatus(HttpServletResponse.SC_OK);
        baseRequest.setHandled(true);
        response.getWriter().println("<h1>Hello World</h1>");
    }
 
    public static void main(String[] args) throws Exception
    {
        Server server = new Server(8080);
        server.setHandler(new HelloWorld());
 
        server.start();
        server.join();
    }
}
Compiling the HelloWord example
The following command compiles the HelloWorld class:

javac -cp servlet-api-2.5.jar:jetty-all-$JETTY_VERSION.jar HelloWorld.java
Running the Handler and Server
The following command runs the HelloWorld example:

java -cp .:servlet-api-2.5.jar:jetty-all-$JETTY_VERSION.jar HelloWorld
You can now point your browser at http://localhost:8080 to see your hello world page.
