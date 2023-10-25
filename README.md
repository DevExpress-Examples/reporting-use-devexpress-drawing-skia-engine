<!-- default badges list -->
![](https://img.shields.io/endpoint?url=https://codecentral.devexpress.com/api/v1/VersionRange/576442348/2023.1)
[![](https://img.shields.io/badge/Open_in_DevExpress_Support_Center-FF7200?style=flat-square&logo=DevExpress&logoColor=white)](https://supportcenter.devexpress.com/ticket/details/T1133108)
[![](https://img.shields.io/badge/📖_How_to_use_DevExpress_Examples-e9f6fc?style=flat-square)](https://docs.devexpress.com/GeneralInformation/403183)
<!-- default badges end -->
## Reporting for ASP.NET Core - How to Use the SkiaSharp-Based DevExpress Drawing Engine

This example demonstrates use of the DevExpress.Drawing package based on the [SkiaSharp](https://github.com/mono/SkiaSharp) library instead of the System.Drawing library in an ASP.NET Core application to preview, [print](https://docs.devexpress.com/XtraReports/15797), or [export](https://docs.devexpress.com/XtraReports/2618) DevExpress Reports-based documents.

The commands required to configure the host operating system environment for the DevExpress Drawing Engine are included in the docker file.

## How to Build and Run This Example

### Visual Studio

You can run the app on the Windows platform, or the Windows Subsystem for Linux or Docker. Select the platform from the Debug drop-down menu in the toolbar and start debugging the app.

### CLI
Run the application from the dotnet CLI on Windows, Linux and MacOS with the `dotnet run` command. To run the Docker container from the command line, build the Docker image. You should pass the DevExpress NuGet source URL as a secret to restore NuGet packages. Review [BuildKit documentation](https://docs.docker.com/build/buildkit/) for additional guidance.

> Windows
>
>```console
>set DX_NUGET=https://nuget.devexpress.com/some-nuget-token/api
>docker build -t reporting-app --secret id=dxnuget,env=DX_NUGET .
>docker run -p 8080:80 reporting-app:latest
>```

> Linux
>
>```shell
>export DX_NUGET=https://nuget.devexpress.com/some-nuget-token/api
>DOCKER_BUILDKIT=1 docker build -t reporting-app --secret id=dxnuget,env=DX_NUGET .
>docker run -p 8080:80 reporting-app:latest
>```

The application page is available at the following URL: `http://localhost:8080/`.

## Files to Review

- [Startup.cs](ReportingWebApp/Startup.cs)

    At startup, call the `DevExpress.Drawing.Internal.DXDrawingEngine.ForceSkia` method to use the **DevExpress Drawing Skia** engine in your application.
- [ReportingWebApp.csproj](ReportingWebApp/ReportingWebApp.csproj)

    The `DockerfileFile` property in the project file specifies the name of the docker file to use in the project. Sample docker files for different operating systems are included in the project. You should edit the project file manually to replace the default **Debian** docker file with docker files for **Alpine**, **Ubuntu**, or **Amazon Linux**. For more information on the build properties in a project file, review the following help topic: [Container Tools build properties](https://docs.microsoft.com/en-us/visualstudio/containers/container-msbuild-properties?view=vs-2022).
- [Dockerfile](ReportingWebApp/Dockerfile)

    **Debian** docker file.
- [Dockerfile.Alpine](ReportingWebApp/Dockerfile.Alpine)

    **Alpine** docker file.
- [Dockerfile.Ubuntu](ReportingWebApp/Dockerfile.Ubuntu)

    **Ubuntu** docker file.
- [Dockerfile.AmazonLinux](ReportingWebApp/Dockerfile.AmazonLinux)

    **Amazon Linux** docker file.
- [Dockerfile.OpenSuse](ReportingWebApp/Dockerfile.OpenSuse)

    **OpenSuse** docker file.

## More Examples

- [How to Use the DevExpress CrossPlatform Drawing Engine in an ASP.NET Core Application](https://github.com/DevExpress-Examples/Reporting-Use-the-DevExpress-CrossPlatform-Drawing-Engine)
