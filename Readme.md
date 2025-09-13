<!-- default badges list -->
![](https://img.shields.io/endpoint?url=https://codecentral.devexpress.com/api/v1/VersionRange/576442348/23.2.3%2B)
[![](https://img.shields.io/badge/Open_in_DevExpress_Support_Center-FF7200?style=flat-square&logo=DevExpress&logoColor=white)](https://supportcenter.devexpress.com/ticket/details/T1133108)
[![](https://img.shields.io/badge/📖_How_to_use_DevExpress_Examples-e9f6fc?style=flat-square)](https://docs.devexpress.com/GeneralInformation/403183)
[![](https://img.shields.io/badge/💬_Leave_Feedback-feecdd?style=flat-square)](#does-this-example-address-your-development-requirementsobjectives)
<!-- default badges end -->
# Reporting for ASP.NET Core - How to Use the SkiaSharp-Based DevExpress Drawing Engine

This example demonstrates how to use the DevExpress.Drawing package based on the [SkiaSharp](https://github.com/mono/SkiaSharp) library instead of the System.Drawing library in an ASP.NET Core application to preview, [print](https://docs.devexpress.com/XtraReports/15797), or [export](https://docs.devexpress.com/XtraReports/2618) DevExpress XtraReports.

The commands required to configure the host operating system environment for the DevExpress Drawing Engine are included in the docker file.

## How to Build and Run this Example

### Specify the NuGet Feed URL for Docker

To restore NuGet packages while building a Docker image, you should pass the DevExpress NuGet feed URL as a secret as follows:

1. Go to [nuget.devexpress.com](https://nuget.devexpress.com) and copy your DevExpress NuGet feed URL.
2. Paste the copied feed URL to the [secrets.dev.yaml](ReportingWebApp/secrets.dev.yaml) file located in the project.

### Run the Example

#### Visual Studio

You can run the app on the Windows platform, or the Windows Subsystem for Linux or Docker. If you want to launch the app with docker, select _Docker_ from the Launch drop-down menu in the Visual Studio toolbar.

#### CLI

Run the application from the dotnet CLI on Windows, Linux, and MacOS with the following command: 

```console
dotnet run
```

To run the Docker container from the command line, build the Docker image:

**Windows**

```console
cd ReportingWebApp
docker build -t reporting-app --secret id=dxnuget,source=secrets.dev.yaml .
docker run -p 8080:80 reporting-app:latest
```

**Linux**

```shell
cd ReportingWebApp
DOCKER_BUILDKIT=1 docker build -t reporting-app --secret id=dxnuget,source=secrets.dev.yaml .
docker run -p 8080:80 reporting-app:latest
```

The application page is available at the following URL: http://localhost:8080/.

Review the Docker documentation for more information: [BuildKit documentation](https://docs.docker.com/build/buildkit/).

> If your secrets.dev.yaml contains the byte order mark (BOM), you can get an error while restoring NuGet packages. To avoid this potential problem, make sure your secrets.dev.yaml encoding does not contain the BOM.

## Files to Review

- [Startup.cs](ReportingWebApp/Startup.cs)

    At startup, call the `DevExpress.Drawing.Internal.DXDrawingEngine.ForceSkia` method to use the **DevExpress Drawing Skia** engine in the application.
- [secrets.dev.yaml](ReportingWebApp/secrets.dev.yaml)

    The file that contains your NuGet feed URL.
- [ReportingWebApp.csproj](ReportingWebApp/ReportingWebApp.csproj)

    The `DockerfileFile` property in the project file specifies the name of the docker file to use in the project. Sample docker files for different operating systems are included in the project. You should edit the project file manually to replace the default **Debian** docker file with docker files for **Alpine**, **Ubuntu** or **Amazon Linux**. For more information on build properties in a project file, review the following help topic: [Container Tools build properties](https://docs.microsoft.com/en-us/visualstudio/containers/container-msbuild-properties?view=vs-2022).
- [Dockerfile](ReportingWebApp/Dockerfile)

    The **Debian** docker file.
- [Dockerfile.Alpine](ReportingWebApp/Dockerfile.Alpine)

    The **Alpine** docker file.
- [Dockerfile.Ubuntu](ReportingWebApp/Dockerfile.Ubuntu)

    The **Ubuntu** docker file.
- [Dockerfile.AmazonLinux](ReportingWebApp/Dockerfile.AmazonLinux)

    The **Amazon Linux** docker file.
- [Dockerfile.OpenSuse](ReportingWebApp/Dockerfile.OpenSuse)

    The **OpenSuse** docker file.

<!-- feedback -->
## Does this example address your development requirements/objectives?

[<img src="https://www.devexpress.com/support/examples/i/yes-button.svg"/>](https://www.devexpress.com/support/examples/survey.xml?utm_source=github&utm_campaign=reporting-use-devexpress-drawing-skia-engine&~~~was_helpful=yes) [<img src="https://www.devexpress.com/support/examples/i/no-button.svg"/>](https://www.devexpress.com/support/examples/survey.xml?utm_source=github&utm_campaign=reporting-use-devexpress-drawing-skia-engine&~~~was_helpful=no)

(you will be redirected to DevExpress.com to submit your response)
<!-- feedback end -->
