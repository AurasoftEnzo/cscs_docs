# CSCS


CSCS_WPF is a scripting programming language based on C# and WPF. Also, cscs_wpf is a completely 'event driven' language.


The initial entry point is to create the first window with the create_window() function or, alternatively, with the directive '#WINFORM path/window_name.xaml' which should be specified at the beginning of the program. If there are several such directives, for example:

```javascript
#winform window1.xaml
#winform window2.xaml
#winform window3.xaml
```

The initial window is the one listed first. Other xaml windows are used only for verification of XAML code.
