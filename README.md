# Getting-return-0-value-from-CSharp
## Getting return 0 value from C# Entry Point Method using Parent and Child Programs

Hello everyone, as we know that in C# Apps (both Console & Win) Entry Point Method refers to the Main() of a program. When the application is started, the Main method is the first method that is invoked. This Main() do have return type as “int” and many of the time we noticed that the return value for this Main() seems to 0. So let’s understand the behind the scene of having this return value in Main().

### Background:
In general, our assumption is (after google search) return 0 in Main() refers to the status code of the application such as  “Exited Successfully” or if it 1 then Exited with some errors. But actually speaking these 0 / 1 is user defined values which is returning to the called program.
### The real benefit of using return 0:
A console app / windows app ends its execution by default GC will perform clean up on all of the allocated resources with respect to the applications. While returning 0 to the OS by the Main() what is the purpose which is seeking by OS? Is it something related with flag bits? Or something kind of process ends? The answer is NO. Because OS never mind the return value from Main() it always considering that the particular application was completed successfully. Okay, then what is the use of returning 0? Yes, here is the role of something like Parent and Child Process come to the place.

This return value can be used when there is a situation when we have Parent and Child Programs. Just assuming that a Parent program called a Child Program, once Child has completed the execution then the program control in Parent process will look for the status (just assuming) of what really happened to the Child Process. Was it completed successfully or it was stalled during program execution. This can be validated by use of “Exit Code” which is returned by the Main(), this Exit code only we are assuming as a flag bit. Let me show this Parent and Child Program with simple example.
Considering Parent Program as Windows App and Child as a Console App. Please follow the steps in order to get the “Exit Code” value (return value).
### Sample Demo Program:
1.	Open Visual Studio (any versions), and create a new project for Windows Application.
2.	Once the project got created, please add another project on top of the above said Windows Application.
3.	The final Project structure looks like below:
         
    ![1](https://user-images.githubusercontent.com/31686277/45375143-c0ca9000-b611-11e8-985b-c682d06c75b6.JPG)
         
4.	In “WindowsAppDemo” project, Add a LabelBox, TextBox and Command button as shown below:

    ![2](https://user-images.githubusercontent.com/31686277/45375144-c1632680-b611-11e8-88e0-a188e2b24ff0.JPG)
    
5.	Add the following code in button click event, in order to call the ConsoleApp which is available in this project solution.

    ![3](https://user-images.githubusercontent.com/31686277/45375145-c1fbbd00-b611-11e8-9e27-d1f673fe62a5.JPG)
    
    In the above, first we have assigned the ChildAppDemo (Console App) to the ProcessStartInfo which is holding the information about the target app.
    
6.	Now, goto “ChildAppDemo” console app, and receive the passing parameter by Windows App and print it on the console. (As shown below).

    ![4](https://user-images.githubusercontent.com/31686277/45375146-c1fbbd00-b611-11e8-83ae-66eaafb45743.JPG)

7.	Currently, our project setup is, We have a Parent program (Windows App) which is internally calling the Child Program (Console App). Make the Parent program (Windows App) as a startup project and will debug the code to see the return value. Let me show you here.

   a)	Once you executed the Windows App, just provide some text and click on the Command Button, Look at the breakpoint here, the Child program is called and still it is running meanwhile if you look at the breakpoint on the called process class, its showing the properties such as “Has Exited” and Exit Code values seems to be unavailable.
   
   ![5](https://user-images.githubusercontent.com/31686277/45375149-c2945380-b611-11e8-991a-006ecc1d71c6.JPG)
   
   b)	Hit enter on the console app , as we written Console.ReadKey() so the Child App (Console app) still remains running, to resume back to the Parent Program (Windows App), Just hit enter on the Console App. Do not press any key except enter, again look at the breakpoint, this time will be getting the exit code as a 0.. This Is the actual benefit of having return values on the Main().
   
   ![6](https://user-images.githubusercontent.com/31686277/45376059-7dbdec00-b614-11e8-9ed9-84ff5fc9508a.JPG)
    
   c)	Final output:
   
   ![7](https://user-images.githubusercontent.com/31686277/45375152-c3c58080-b611-11e8-8937-94c862b1f6c5.JPG)
   
   You can give return integer value as anything. The same value can be received from “ExitCode” property. 
   
## Conclusion:
So, this what I tried to share the details about having return 0 in the Main(). This is just an experimental program. Can be used suppose we do have cascade console apps in a solution and it has be called one by one means we can validate the cascading called projects by using “Exit Code” property.

*Thanks much for reading this article.*

## Happy Coding!
  
  
  
  
  
  
  
  
