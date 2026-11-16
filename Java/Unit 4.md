
# **==🔴APPLET==**
**What is an Applet?**
An Applet is a small Java program that runs inside a web browser or an applet viewer. It is mainly used to create interactive applications and graphical content.

==🔴**Important modern Java note**==
Java Applets are obsolete. The Applet API was deprecated in Java 9 and removed in Java 26. Modern browsers also no longer support Java applets.

## **Features of Applet**

1. Applets are written in Java.
2. They were designed to run inside web browsers.
3. They support graphical user interfaces (GUI).
4. They can handle mouse and keyboard events.
5. They do not have a `main()` method as their entry point.
6. They use a predefined life cycle.

![[Pasted image 20261117002028.png|439]]

![[Pasted image 20261117002227.png]]

## **Advantages of Applet**

- Platform independent.
- Supports graphical applications.
- Supports event handling.
- Provides a controlled execution environment.

## **Disadvantages of Applet**

- Requires an applet-compatible environment.
- Has limited access to system resources.
- Modern browsers do not support Java applets.
- Requires additional setup to execute.


```
import java.applet.*;

import java.awt.*;

import java.awt.event.*;

  

public class applet extends Applet implements ActionListener {
	TextField t1 = new TextField(5);
	TextField t2 = new TextField(5);
	TextField t3 = new TextField(5);

	Label l1 = new Label("num1");
	Label l2 = new Label("num2");
	Label l3 = new Label("result");
	
	Button b = new Button("sum");

	public void init() {
		add(l1); add(t1);
		add(l2); add(t2);
		add(l3); add(t3);
		add(b);
		b.addActionListener(this);
	}

	public void actionPerformed(ActionEvent e) {

	try { // fixed: handle bad input
		int n1 = Integer.parseInt(t1.getText().trim());
		int n2 = Integer.parseInt(t2.getText().trim());
		t3.setText("" + (n1 + n2));
	} catch (NumberFormatException ex) {
		t3.setText("Invalid!");
		}
	}
}
```

## **Quick Revision**

- **Applet:** Small Java program that historically ran inside a browser or applet viewer.
- **Parent class:** `Applet`
- **Package:** `java.applet`
- **Graphics package:** `java.awt`
- **Entry point:** No `main()` method.
- **Lifecycle:** `init()`, `start()`, `paint()`, `stop()`, `destroy()`.



# ==🟠**AWT (Abstract Window Toolkit)**==

**English Definition:** AWT is a Java GUI toolkit that provides classes and components for creating graphical user interfaces. It uses native operating system components to display GUI elements.

**AWT Packages**

```
import java.awt.*;
import java.awt.event.*;
```

- `java.awt` – GUI components, layouts, graphics, etc.
- `java.awt.event` – Event handling such as button clicks and mouse events.

**Important AWT Classes and Components**


![[Pasted image 20261117003312.png|407]]![[Pasted image 20261117003350.png|408]]

### CODE :

```java
import java.awt.*;
import java.awt.event.*;

class AWTForm extends Frame {

    AWTForm() {
        setTitle("Student Registration Form");
        setSize(350, 300);
        setLayout(new FlowLayout());

        Label nameLabel = new Label("Name:");
        TextField nameField = new TextField(20);

        Label ageLabel = new Label("Age:");
        TextField ageField = new TextField(20);

        Label genderLabel = new Label("Gender:");
        CheckboxGroup gender = new CheckboxGroup();

        Checkbox male = new Checkbox("Male", gender, false);
        Checkbox female = new Checkbox("Female", gender, false);

        Button submit = new Button("Submit");

        add(nameLabel);
        add(nameField);
        add(ageLabel);
        add(ageField);
        add(genderLabel);
        add(male);
        add(female);
        add(submit);

        submit.addActionListener(e ->
            System.out.println("Form Submitted!")
        );

        addWindowListener(new WindowAdapter() {
            public void windowClosing(WindowEvent e) {
                dispose();
            }
        });

        setVisible(true);
    }

    public static void main(String[] args) {
        new AWTForm();
    }
}
```


# ==🟠**Swing in Java**==

**English Definition:** Swing is a part of Java Foundation Classes (JFC) that provides a set of lightweight, platform-independent GUI components for developing desktop applications.

**Swing Package**
```
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
```

- `javax.swing` – Swing GUI components.
- `java.awt` – Layouts, colors, fonts, graphics, etc.
- `java.awt.event` – Event handling.

## **Important Swing Classes and Components**

![[Pasted image 20261117003718.png]]![[Pasted image 20261117003734.png|579]]

### CODE :

```java
import javax.swing.*;

class SwingForm {

    SwingForm() {
        JFrame frame = new JFrame("Student Registration Form");

        frame.setSize(350, 300);
        frame.setLayout(null);

        JLabel nameLabel = new JLabel("Name:");
        nameLabel.setBounds(30, 30, 80, 25);

        JTextField nameField = new JTextField();
        nameField.setBounds(120, 30, 150, 25);

        JLabel ageLabel = new JLabel("Age:");
        ageLabel.setBounds(30, 70, 80, 25);

        JTextField ageField = new JTextField();
        ageField.setBounds(120, 70, 150, 25);

        JLabel genderLabel = new JLabel("Gender:");
        genderLabel.setBounds(30, 110, 80, 25);

        JRadioButton male = new JRadioButton("Male");
        male.setBounds(120, 110, 70, 25);

        JRadioButton female = new JRadioButton("Female");
        female.setBounds(190, 110, 90, 25);

        ButtonGroup group = new ButtonGroup();
        group.add(male);
        group.add(female);

        JButton submit = new JButton("Submit");
        submit.setBounds(120, 160, 100, 30);

        submit.addActionListener(e ->
            JOptionPane.showMessageDialog(frame, "Form Submitted!")
        );

        frame.add(nameLabel);
        frame.add(nameField);
        frame.add(ageLabel);
        frame.add(ageField);
        frame.add(genderLabel);
        frame.add(male);
        frame.add(female);
        frame.add(submit);

        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setVisible(true);
    }

    public static void main(String[] args) {
        new SwingForm();
    }
}
```

==🔴NOTE :== This uses `javax.swing` (lightweight components). Unlike AWT, Swing components are platform-independent and offer a more modern look. For production forms, consider using layout managers (e.g., `GridBagLayout`, `GridLayout`) instead of `null` layout for better resizing behaviour.



# ==🟠**Window Fundamentals in Java**==

## **Detailed Definition**

**Window Fundamentals** in Java refer to the basic concepts and components used to create, display, manage, and control graphical windows in a Java GUI application.

A window is a rectangular area displayed on the screen where users can interact with an application through components such as buttons, labels, text fields, menus, and other GUI elements.

Java provides the **AWT (Abstract Window Toolkit)** and **Swing** libraries to create and manage windows.

In AWT, the `Frame` class is commonly used to create a window, whereas in Swing, the `JFrame` class is used.

![[Pasted image 20261117005140.png]]
![[Pasted image 20261117005155.png|560]]

# My First Window (AWT)

A minimal Java AWT program that displays a simple window with a welcome label and a clickable button.

## Code

```java
import java.awt.*;

class MyWindow {
    public static void main(String[] args) {
        Frame f = new Frame("My First Window");
        f.setSize(400, 300);
        f.setLayout(new FlowLayout());
        Label l = new Label("Welcome to Java");
        Button b = new Button("Click Me");
        f.add(l);
        f.add(b);
        f.setVisible(true);
    }
}
```

![[Pasted image 20261117005426.png]]


# **Delegation Event Model in Java**

## **Definition**

The **Delegation Event Model (DEM)** is an event-handling mechanism in Java used to handle user interactions with GUI components.

In this model, the component that generates an event does not handle the event itself. Instead, it delegates the responsibility of handling that event to a separate object called an **Event Listener**.

The Delegation Event Model was introduced in **Java 1.1** and is used in both AWT and Swing.

For example, when a user clicks a button, the button generates an event. A registered listener receives that event and executes the required code.

### **Main Components of Delegation Event Model**

There are three main components:

**1. Event Source**

The object that generates an event due to user interaction.

Examples:

- Button
- Text Field
- Checkbox
- Window

**2. Event Object**

An object that contains information about the event that occurred.

Examples:

- `ActionEvent`
- `MouseEvent`
- `KeyEvent`
- `WindowEvent`
- `ItemEvent`

**3. Event Listener**

An object that waits for an event and handles it when it occurs.

Examples:

- `ActionListener`
- `MouseListener`
- `KeyListener`
- `WindowListener`
- `ItemListener`

![[Pasted image 20261117010127.png]]

![[Pasted image 20261117010213.png]]

# Event Handling in AWT (Delegation Event Model)

A Java AWT program demonstrating event handling using the **Delegation Event Model**, where a button click is captured and handled by a registered listener.

## Code

```java
import java.awt.*;
import java.awt.event.*;

class EventDemo extends Frame implements ActionListener {

    Button b;

    EventDemo() {
        setTitle("Event Handling");
        setSize(300, 200);
        setLayout(new FlowLayout());

        b = new Button("Click Me");

        // Register listener
        b.addActionListener(this);

        add(b);

        setVisible(true);
    }

    // Event handling method
    public void actionPerformed(ActionEvent e) {
        System.out.println("Button Clicked!");
    }

    public static void main(String[] args) {
        new EventDemo();
    }
}
```

## Explanation of the Code

1. **`Button b`** creates a button.
2. **`implements ActionListener`** means the class can handle action events.
3. **`addActionListener(this)`** registers the current object as the listener.
4. When the button is clicked, an **`ActionEvent`** is generated.
5. **`actionPerformed()`** is automatically called to handle the event.

## Advantages of the Delegation Event Model

1. **Separation of responsibility** – Event generation and event handling are separate.
2. **Flexibility** – Different listeners can handle different types of events.
3. **Reusability** – Listener objects can be reused.
4. **Efficiency** – Events are delivered to registered listeners rather than requiring every component to continuously check for events.
5. **Easy maintenance** – Event-handling code can be managed separately.


## **Introduction to Event Handling**

**Definition:**

Event handling in Java is a mechanism used to detect and respond to user interactions with GUI (Graphical User Interface) components. These interactions are called events.

Events can be generated through different input devices, such as a mouse and keyboard. Java provides event listener interfaces to handle these events.

For example:

- Clicking a mouse button.
- Moving the mouse pointer.
- Pressing a keyboard key.
- Releasing a key.
- Typing characters into a text field.

Java uses the **Delegation Event Model** to handle mouse and keyboard events.

**Easy Explanation:** Event handling means making a Java program respond when a user performs an action, such as clicking a button or pressing a key.

# ==🟢**Mouse Event Handling**==

## **Definition  :** 
Mouse event handling in Java is the process of detecting and responding to actions performed using a mouse.

Java provides the `MouseListener` and `MouseMotionListener` interfaces in the `java.awt.event` package to handle mouse events.

These interfaces allow a program to detect mouse clicks, pressing, releasing, entering, exiting, movement, and dragging.

## **MouseListener Interface**

The `MouseListener` interface is used to handle basic mouse actions.

It contains five important methods:

|Method|Description|
|---|---|
|`mouseClicked()`|Called when the mouse button is clicked.|
|`mousePressed()`|Called when a mouse button is pressed.|
|`mouseReleased()`|Called when a pressed mouse button is released.|
|`mouseEntered()`|Called when the mouse pointer enters a component.|
|`mouseExited()`|Called when the mouse pointer leaves a component.|
## **MouseMotionListener Interface**

The `MouseMotionListener` interface is used to detect mouse movement and dragging.

It contains two methods:

|Method|Description|
|---|---|
|`mouseMoved()`|Called when the mouse pointer moves without pressing a button.|
|`mouseDragged()`|Called when the mouse pointer moves while a mouse button is pressed.|

**Difference:**

- `mouseMoved()` → Moving the mouse normally.
- `mouseDragged()` → Moving the mouse while holding a mouse button.

## **MouseEvent Class**

The `MouseEvent` class represents mouse-related events.

It provides information about the mouse action, such as:

|Method|Purpose|
|---|---|
|`getX()`|Returns the X-coordinate of the mouse pointer.|
|`getY()`|Returns the Y-coordinate of the mouse pointer.|
|`getClickCount()`|Returns the number of mouse clicks.|
|`getButton()`|Returns which mouse button was used.|

For example, `e.getX()` and `e.getY()` can be used to find the mouse pointer's position.

# Mouse Event Handling in AWT

A Java AWT program that demonstrates **mouse event handling** using the `MouseListener` interface. The label text updates dynamically as the user performs different mouse actions on the window.

## Code

```java
import java.awt.*;
import java.awt.event.*;

class MouseDemo extends Frame implements MouseListener {

    Label l;

    MouseDemo() {
        setTitle("Mouse Event Demo");
        setSize(400, 300);
        setLayout(new FlowLayout());

        l = new Label("Perform Mouse Actions");

        add(l);

        addMouseListener(this);

        setVisible(true);
    }

    public void mouseClicked(MouseEvent e) {
        l.setText("Mouse Clicked");
    }

    public void mousePressed(MouseEvent e) {
        l.setText("Mouse Pressed");
    }

    public void mouseReleased(MouseEvent e) {
        l.setText("Mouse Released");
    }

    public void mouseEntered(MouseEvent e) {
        l.setText("Mouse Entered");
    }

    public void mouseExited(MouseEvent e) {
        l.setText("Mouse Exited");
    }

    public static void main(String[] args) {
        new MouseDemo();
    }
}
```
**Code Explanation:**

1. `implements MouseListener` allows the class to handle mouse events.
2. `addMouseListener(this)` registers the current object as a mouse listener.
3. `MouseEvent e` contains information about the mouse event.
4. Each mouse method executes when its corresponding event occurs.
5. `l.setText()` changes the displayed message.

# **Keyboard Event Handling**

## **Detailed Definition**

Keyboard event handling in Java is the process of detecting and responding to actions performed using a keyboard.

Java provides the `KeyListener` interface in the `java.awt.event` package to handle keyboard events.

It allows a program to detect when a key is pressed, released, or typed.

For example:

- Pressing the Enter key.
- Releasing the Shift key.
- Typing letters or numbers.
- Pressing arrow keys to control a game character.

## **A.KeyListener Interface**

The `KeyListener` interface contains three important methods:

|Method|Description|
|---|---|
|`keyPressed()`|Called when a keyboard key is pressed.|
|`keyReleased()`|Called when a pressed key is released.|
|`keyTyped()`|Called when a character is typed.|

## **B.KeyEvent Class**

The `KeyEvent` class represents keyboard-related events.

It provides information about which key was pressed, released, or typed.

Important methods:

|Method|Purpose|
|---|---|
|`getKeyChar()`|Returns the character associated with the key event.|
|`getKeyCode()`|Returns the integer key code.|
|`getKeyText()`|Returns the text representation of a key code.|
|`isActionKey()`|Checks whether the key is an action key, such as an arrow key.|

**Example:**

- `getKeyChar()` → Returns `'A'`.
- `getKeyCode()` → Returns the key code for the A key.
- `getKeyText()` → Returns `"A"` for the corresponding key code.


## **C. Keyboard Event Handling Program**

## Code

```java
import java.awt.*;
import java.awt.event.*;

class KeyboardDemo extends Frame implements KeyListener {

    Label l;

    KeyboardDemo() {
        setTitle("Keyboard Event Demo");
        setSize(400, 300);
        setLayout(new FlowLayout());

        l = new Label("Press any key");

        add(l);

        addKeyListener(this);

        setFocusable(true);
        requestFocus();

        setVisible(true);
    }

    public void keyPressed(KeyEvent e) {
        l.setText("Key Pressed: " + e.getKeyChar());
    }

    public void keyReleased(KeyEvent e) {
        l.setText("Key Released: " + e.getKeyChar());
    }

    public void keyTyped(KeyEvent e) {
        l.setText("Key Typed: " + e.getKeyChar());
    }

    public static void main(String[] args) {
        new KeyboardDemo();
    }
}
```

## Explanation of the Code

1. **`implements KeyListener`** – The class must implement all **3 abstract methods** of the `KeyListener` interface.
2. **`addKeyListener(this)`** – Registers the frame as the keyboard listener.
3. **`setFocusable(true)`** – Makes the frame capable of receiving keyboard focus (required for key events).
4. **`requestFocus()`** – Explicitly requests focus so the frame becomes the active input target.
5. **`e.getKeyChar()`** – Returns the character representation of the key that was pressed/released/typed.
6. **`setText()`** – Updates the label so the user sees live feedback in the GUI.

