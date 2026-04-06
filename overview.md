# Java Programming — Quick Notes

---

## 1. Introduction

Java is a **compiled, object-oriented** language that runs on the **Java Virtual Machine (JVM)**, making it platform-independent ("write once, run anywhere").

Key components:
- **JDK** (Java Development Kit) — tools to write and compile Java code
- **JRE** (Java Runtime Environment) — runs compiled Java programs
- **JVM** (Java Virtual Machine) — executes the bytecode

---

## 2. Environment Setup

### Installing Java on Windows

**Option A — Installer (recommended for beginners)**

1. Go to [adoptium.net](https://adoptium.net) and download the **Windows x64 `.msi` installer** (LTS version recommended, e.g. Java 21).
2. Run the installer — check **"Set JAVA_HOME variable"** and **"Add to PATH"** options during setup.
3. Restart your terminal/Command Prompt after installation.

**Option B — Winget (terminal)**
```powershell
winget install EclipseAdoptium.Temurin.21.JDK
```

**Verify installation:**
```cmd
java -version
javac -version
```

**Manually set `JAVA_HOME` if needed:**
1. Search **"Environment Variables"** in the Start menu.
2. Under *System Variables*, click **New** → Name: `JAVA_HOME`, Value: your JDK path (e.g. `C:\Program Files\Eclipse Adoptium\jdk-21`).
3. Find the `Path` variable → Edit → Add `%JAVA_HOME%\bin`.

---

### Installing Java on macOS

**Option A — Homebrew (recommended)**
```bash
# Install Homebrew first if you don't have it
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install JDK (Temurin 21 LTS)
brew install --cask temurin@21
```

**Option B — Installer**
1. Go to [adoptium.net](https://adoptium.net), download the **macOS `.pkg` installer**.
2. Double-click and follow the prompts — PATH is set automatically.

**Verify installation:**
```bash
java -version
javac -version
```

**`JAVA_HOME` on macOS** (add to `~/.zshrc` or `~/.bash_profile`):
```bash
export JAVA_HOME=$(/usr/libexec/java_home)
export PATH=$JAVA_HOME/bin:$PATH
```
Then reload: `source ~/.zshrc`

---

### Verify Your Setup (Both Platforms)

Both commands should return version numbers:

```bash
java -version
javac -version
```

Expected output (version may differ):
```
openjdk version "21.0.x" ...
javac 21.0.x
```

> If `javac` is not found but `java` works, you installed a **JRE** instead of a **JDK**. Re-install using the steps above and select the JDK package.

---

## 3. Creating Your First Java Program

Every Java program lives inside a **class**. The `main` method is the entry point — execution always starts here.

**`HelloWorld.java`**
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

> **Rule:** The filename must match the class name exactly, including capitalisation.

### Breaking it down

| Part | What it means |
|---|---|
| `public class HelloWorld` | Defines a class named `HelloWorld` |
| `public static void main(String[] args)` | Entry point the JVM looks for |
| `System.out.println(...)` | Prints a line to the console |

---

## 4. Compiling Your Java Program

Compilation converts `.java` source code into `.class` bytecode the JVM can execute.

```bash
# Compiles the file → produces HelloWorld.class
javac HelloWorld.java
```

If there are no errors, a `HelloWorld.class` file appears in the same directory.

---

## 5. Running Your Java Program

Pass the **class name** (not the filename) to the `java` command. Do **not** include the `.class` extension.

```bash
# Runs the program
java HelloWorld
# Output: Hello, World!
```

### The compile → run cycle

```
HelloWorld.java  →  javac  →  HelloWorld.class  →  java  →  Output
  (source code)               (bytecode)                    (console)
```

---

## 6. Modifying Your Program — User Input with Scanner

The `Scanner` class (from `java.util`) lets you read input from the keyboard.

**`InteractiveGreeting.java`**
```java
import java.util.Scanner;

public class InteractiveGreeting {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter your name: ");
        String name = scanner.nextLine();

        System.out.println("Hello, " + name + "!");

        scanner.close(); // Good practice to close the scanner
    }
}
```

### Key Scanner methods

| Method | Reads |
|---|---|
| `nextLine()` | Full line of text (String) |
| `nextInt()` | An integer |
| `nextDouble()` | A decimal number |
| `next()` | Single word (whitespace-delimited) |

> Always call `scanner.close()` when you're done — it frees the underlying resource.

---

## 7. Quick Reference

```bash
# Compile
javac FileName.java

# Run
java ClassName

# Check versions
java -version
javac -version
```

### Common beginner mistakes

- Forgetting the semicolon `;` at the end of statements
- Filename not matching the class name
- Running `java HelloWorld.class` instead of `java HelloWorld`
- Forgetting to `import java.util.Scanner` when using Scanner

---

## 8. Comments in Java

```java
// Single-line comment

/* Multi-line
   comment */

/**
 * Javadoc comment — used for documentation
 */
```

---

*These notes cover Day 1 fundamentals. Next up: variables, data types, and control flow.*
