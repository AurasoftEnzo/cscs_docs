# Welcome to CSCS Documentation

**CSCS** (Custom Scripting in C#) is a scripting language implemented in C#.


## What is CSCS?

CSCS is designed to provide a flexible scripting solution that integrates seamlessly with .NET ecosystems.

## Quick Example

<!-- ### Heading 3

#### Heading 4

### Heading 3 -->

```javascript
// A simple CSCS script
a = 5;
b = 10;
result = a + b;
print("The result is: ", result);
```


## Installation

Download the latest CSCS interpreter from the releases page.

## Your First Script

1. Create a file called `hello.cscs`
2. Add the following code:
```javascript
print("Hello, CSCS!");
```
3. asdlkajsdl


```javascript
// Variable declarations
name = "John";
age = 25;
height = 5.9;
isActive = true;

// Reassigning variables
counter = 0;
counter = counter + 1;
```

```xml
<Window 
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:TestiranjeTextboxEvenata"
        mc:Ignorable="d"
        Title="Window1" Height="450" Width="800">
    <Grid>
        <DataGrid HorizontalAlignment="Center" VerticalAlignment="Center" Height="300" Width="300" AutoGenerateColumns="False" DataContext="grid1">
            <DataGrid.Columns>
            <DataGridTextColumn  Header="array1"/>
            <DataGridTextColumn  Header="array2"/>
            <DataGridTextColumn  Header="array3"/>
           <!--     
               <DataGridTemplateColumn Header="head1">
                    <DataGridTemplateColumn.CellTemplate>
                        <DataTemplate>
                            <TextBox  DataContext ="Variable3"  />
                        </DataTemplate>
                    </DataGridTemplateColumn.CellTemplate>
                </DataGridTemplateColumn>
                <DataGridTemplateColumn Header="head2" >
                    <DataGridTemplateColumn.CellTemplate>
                        <DataTemplate>
                            <DatePicker  DataContext ="Variable2" />
                        </DataTemplate>
                    </DataGridTemplateColumn.CellTemplate>
                </DataGridTemplateColumn>
                <DataGridTemplateColumn Header="head3">
                    <DataGridTemplateColumn.CellTemplate>
                        <DataTemplate>
                            <CheckBox  DataContext ="Variable3"  />
                        </DataTemplate>
                    </DataGridTemplateColumn.CellTemplate>
                </DataGridTemplateColumn> 
                -->
            </DataGrid.Columns>
        </DataGrid>
        
    </Grid>
</Window>
```

```c#
class SetWindowModalResultFunction : ParserFunction
{
	protected override Variable Evaluate(ParsingScript script)
	{
		List<Variable> args = script.GetFunctionArgs();
		Utils.CheckArgs(args.Count, 1, m_name);

		//var windowName = Utils.GetSafeString(args, 0);
		var modalResult = Utils.GetSafeVariable(args, 0).AsBool();

		var gui = CSCS_GUI.GetInstance(script);

		var scriptWindow = gui.GetScriptWindow(script);
		scriptWindow.DialogResult = modalResult;

		return Variable.EmptyInstance;
	}
}   
```


<!-- # CSCS(Wpf) extended for TAS (Manual) -->

## Heading 2 - DESCRIPTION OF CSCS

CSCS (Customized Scripting in C#) is a scripting language framework, which is very easy to integrate into any C# project and adjust according to your needs. Basically, the concept of CSCS is not only a language, but also a framework that you can use to create your own language. Since the compiler will be inside of your project, you can do whatever you want with the language: add new features, modify existing ones, etc.

### 3333

- The syntax is a mixture between C#, JavaScript, and Python.
- All statements must end with a semicolon ";".
- Identation and new lines are not used in parsing (unlike Python).
- All CSCS variables have at least 3 properties that can be accessed using the dot notation: properties, type, size, and string.
- Variables and arrays are all defined implicitly, e.g. x=5, b[7]=11
 An example of a list initialization: c = {"aa", "bb", "xxx"};
 You can also define it explicitly: c[0]="aa"; c[1]="bb";
 Definition in index form doesn't have to start from index 0, or even from the first dimension: not defined elements will have a type NONE. E.g.: b[5][3][5][3]=15;
 Similarly, when defining dictionaries, e.g.: x["bla"]["blu"]="wichtig";
- Control flow statements if, else, while, for, try, etc., all require statements between the curly braces (even for a single statement).
- "elif" means "else if" (like in Python)


[funcs](reference/functions/)