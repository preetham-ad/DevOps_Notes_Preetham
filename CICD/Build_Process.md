# Understanding the Build Process

## Compiling Code

**Compiling** is like turning a recipe into a meal. Here's how it works:

- **Source Code**: Think of source code as a recipe written in a programming language (like Java or C++).
- **Compiler**: A compiler is like a chef who reads the recipe and prepares the dish. The chef (compiler) translates the recipe (source code) into something that can be served (executed by the computer).

So, compiling means converting the code you’ve written into a form that the computer can understand and run. This usually involves turning it into machine code or bytecode.

## Executable Formats

**Executable formats** are like the finished meal that’s ready to be served:

- **Executable Files**: These are files that the computer can directly run. For example, a file with a `.exe` extension on Windows or an executable file on Unix/Linux systems.
- **Bytecode**: For languages like Java, the code is first compiled into bytecode, which can be run by a special program called the Java Virtual Machine (JVM).

In essence, an executable format is the final product you get after compiling, which the computer can run to perform the tasks you’ve programmed.

## Deployable Artifacts

**Deployable artifacts** are like the packaged meal ready for delivery:

- **Packaged Code**: After compiling the code, the build process often packages it together with all its necessary components (like libraries, configuration files) into a neat bundle.
- **Examples**: These packages could be an installer, a ZIP file containing the compiled code, or a Docker container image.

A deployable artifact is the final bundle that you can deploy to a server, distribute to users, or use in a production environment. It’s everything you need to get your application running on another system.

## Putting It All Together

- **Compiling**: Takes your code and turns it into something the computer can run.
- **Executable Formats**: The result of compiling, which is a file the computer can directly execute.
- **Deployable Artifacts**: The complete package that includes the executable code and everything else needed to run your app.

## Example

Imagine you’re making a cake:

- **Recipe (Source Code)**: Your recipe is written in a cookbook (source code).
- **Chef (Compiler)**: The chef follows the recipe and bakes the cake (compiling).
- **Cake (Executable Format)**: The cake is ready to eat (executable format).
- **Cake Box (Deployable Artifact)**: The cake is packaged in a box for delivery (deployable artifact).

So, compiling converts your recipe into a cake, executable formats are the ready-to-eat cake, and deployable artifacts are the cake boxed up and ready to be sent out.
