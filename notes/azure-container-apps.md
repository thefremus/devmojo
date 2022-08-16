# Azure Container Apps

I want to take some time to consider Azure Container Apps by building a sample application. The goal is to understand the technology behind it. As a starting thought - the benefit of serverless vs containers - with containers you give the application everything it needs to run. You can, for instance, run nginx with .NET Core on a container. Serverless does not work that way.

## The basics

### What are containers?

> In technical terms, containers are a way of partitioning a machine, or server, into separate user space environments such that each environment runs only one application and doesn’t interact with any other partitioned sections on the machine. Each container shares the machine's kernel with other containers (the kernel is the foundation of the operating system, and it interacts with the computer's hardware), but it runs as if it were the only system on the machine.

> Containers are all the rage now-a-days and for good reason. They solve the problem of how to have an application work consistently regardless of the environment it is run on. This is achieved by bundling the whole runtime environment - the application, it's dependancies, configuration files, etc... Into a single image. This image can then be shared and instances of it, known as containers, can then be run.  

> Docker is a platform which provides services and tools to allow the building, sharing and running of containers. These containers are isolated from one another but run on a shared OS kernel, making them far more lightweight than virtual machines. This allows more containers to be run on the same physical hardware giving containers an advantage over traditional virtual machines.

> As containers only contain what is needed to run the application it makes them extremely quick to spin up. This makes them exceptionally good at scaling on demand. Where a traditional VM would need a few minutes before additional capacity comes online, a container can be started in a few fractions of a second.

### What about virtual machines?

> A virtual machine is a piece of software that imitates a complete computer system. It is isolated from the rest of the machine that hosts it and behaves as if it were the only operating system on it, including having its own kernel. Virtual machines are another common way of hosting multiple environments on one server, but they use a lot more processing power than containers.

## What is Blazor then again?

[From the official docs](https://dotnet.microsoft.com/en-us/apps/aspnet/web-apps/blazor). 

> Blazor lets you build interactive web UIs using C# instead of JavaScript. Blazor apps are composed of reusable web UI components implemented using C#, HTML, and CSS. Both client and server code is written in C#, allowing you to share code and libraries.

> Blazor can run your client-side C# code directly in the browser, using WebAssembly. Because it's real .NET running on WebAssembly, you can re-use code and libraries from server-side parts of your application.

> Alternatively, Blazor can run your client logic on the server. Client UI events are sent back to the server using SignalR - a real-time messaging framework. Once execution completes, the required UI changes are sent to the client and merged into the DOM. The document object model(DOM) is a programming interface that represents all elements on an HTML page as nodes in a tree structure. Using the DOM, elements can be updated, added, and removed from the page.

> Build native apps with Blazor Hybrid
Build native client apps using existing Blazor web UI components with Blazor Hybrid. Share the same Blazor components across mobile, desktop, and web while taking advantage of full access to native client capabilities. Use Blazor Hybrid to build cross-platform apps with .NET MAUI, or to modernize existing WPF and Windows Forms apps.

> Blazor apps can use existing .NET libraries, thanks to .NET Standard—a formal specification of .NET APIs that are common across all .NET implementations.

> .NET Standard allows the same code and libraries to be used on the server, in the browser, or anywhere you write .NET code.

## Blazor in a Docker Container

For the sample I am doing I am following along with [Containerising Blazor Applications With Docker (Part 1)](https://chrissainty.com/containerising-blazor-applications-with-docker-containerising-a-blazor-server-app/). 

- Step 1: Create a vanilla Blazor Server App
- Step 2: Add Docker Support
- Step 3: Build the image
- Step 4: Run the container

## References

- [Serverless computing vs. containers](https://www.cloudflare.com/learning/serverless/serverless-vs-containers/)
- [Containerising Blazor Applications With Docker (Part 1)](https://chrissainty.com/containerising-blazor-applications-with-docker-containerising-a-blazor-server-app/)