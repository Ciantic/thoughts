---
title: 'WPF Command line arguments.'
date: 2009-10-05T14:29:00.000-07:00
oldUrl: "http://ciantic.blogspot.com/2009/10/wpf-command-line-arguments.html"
tags : [wpf codesnippet]
---

**App.xaml**
```
<Application ...
Startup="App_Startup">
```
  

**App.xaml.cs**  
```c#
// ...
/// <summary>  
/// Interaction logic for App.xaml  
/// </summary>  
public partial class App : Application  
{  
    // Storing your arguments in your type you wish:  
    public static string Input = "";  
  
    void App_Startup(object sender, StartupEventArgs e)  
    {  
        // Store the arguments to static public you declared:  
        Input = String.Join(" ", e.Args);  
    }  
}  
// ...
```

**Window1.xaml.cs**  
```c#  
    /// <summary>  
    /// Create window.  
    /// </summary>  
    public Window1()  
    {  
        Console.WriteLine(App.Input); // Woohoo! Got the input...  
        ...  
```

See, MSDN, you don't have to be so damn verbose always, when little **codespeak** would do.