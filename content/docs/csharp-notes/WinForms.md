---
weight: 2
title: "WinForms"
description: ""
icon: "article"
date: "2025-03-09"
lastmod: "2025-03-11"
draft: false
toc: true
---
{{< alert context="info" 
	text="WinForms Quick References with definitions & examples." />}}

## Core WinForm Classes

### Form
A Form is the main window in a Windows Form application. Every WinForms app has at least one Form.
```csharp
using System;
using System.Windows.Forms;

public class MyForm : Form
{
    public MyForm()
    {
        this.Text = "My Custom WinForms Window"; // Sets window title
        this.Width = 500; // Sets window width
        this.Height = 400; // Sets window height
        this.StartPosition = FormStartPosition.CenterScreen; // Centers window on startup
    }
}

// Entry Point
public static class Program
{
    [STAThread]
    static void Main()
    {
        Application.EnableVisualStyles();
        Application.Run(new MyForm()); // Starts the application with MyForm
    }
}
```
- A form is a top-level window in the WinForms UI.
- You can create multiple forms and switch between them.

### Application
The Application class manages the lifecycle of a WinForms application (startup, shutdown, message loop, etc.).
```csharp
using System;
using System.Windows.Forms;

public class MyApp : Form
{
    public MyApp()
    {
        this.Text = "Application Lifecycle Example";

        Button btnExit = new Button();
        btnExit.Text = "Exit";
        btnExit.Click += (s, e) => Application.Exit(); // Closes the application
        this.Controls.Add(btnExit);
    }
}

// Entry Point
public static class Program
{
    [STAThread]
    static void Main()
    {
        Application.EnableVisualStyles(); // Enables modern rendering
        Application.SetCompatibleTextRenderingDefault(false);
        Application.Run(new MyApp()); // Runs the application
    }
}
```
- Application.Run(new Form()) -> Starts the message loop for the form.
- Application.Exit() -> Closes the application.

### Control
The Control class is the foundation for all WinForms UI elements (e.g., buttons, labels, textboxes).
```csharp
using System.Windows.Forms;
using System.Drawing;

public class CustomControl : Control
{
    protected override void OnPaint(PaintEventArgs e)
    {
        base.OnPaint(e);
        e.Graphics.FillRectangle(Brushes.Blue, this.ClientRectangle); // Draws a blue rectangle
    }
}

// Using the Custom Control
public class MainForm : Form
{
    public MainForm()
    {
        this.Text = "Control Example";
        CustomControl myControl = new CustomControl();
        myControl.Size = new Size(200, 100);
        this.Controls.Add(myControl);
    }
}
```
- All UI components derive from Control (e.g., Button, TextBox, etc.).
- Provides properties like Size, BackColor, Enabled, etc.

### ContainerControl
A ContainerControl is a special type of control that contains other controls.
Examples: Form, Panel, UserControl
```csharp
Panel panel = new Panel();
panel.Size = new Size(200, 100);
panel.BackColor = Color.LightGray;
this.Controls.Add(panel);

Button insideButton = new Button();
insideButton.Text = "Inside Panel";
panel.Controls.Add(insideButton);
```
- Used for organizing UI elements into sections.
- Forms and UserControls inherit from ContainerControl.

### UserControl
A UserControl is a reusable, custom control that you can use in multiple forms.
```csharp
using System.Windows.Forms;
using System.Drawing;

public class MyUserControl : UserControl
{
    public MyUserControl()
    {
        this.Size = new Size(200, 100);
        this.BackColor = Color.AliceBlue;
        Label label = new Label { Text = "Hello, UserControl!", AutoSize = true };
        this.Controls.Add(label);
    }
}

// Using the UserControl in a Form
public class MainForm : Form
{
    public MainForm()
    {
        this.Text = "UserControl Example";
        MyUserControl myControl = new MyUserControl();
        this.Controls.Add(myControl);
    }
}
```
- Used for encapsulating reusable UI logic.
- Encapsulates controls like button, textboxes, etc.

### MessageBox
A MessageBox is a built-in pop-up window for alerts, confirmations, and messages.
```
DialogResult result = MessageBox.Show("Do you want to continue?", "Confirm", MessageBoxButtons.YesNo, MessageBoxIcon.Question);

if (result == DialogResult.Yes)
{
    MessageBox.Show("You clicked Yes!");
}
else
{
    MessageBox.Show("You clicked No.");
}

```
- Shows messages to the user.
- Supports different buttons (OK, Yes/No, Retry/Cancel)