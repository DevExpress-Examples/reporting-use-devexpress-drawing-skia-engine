## Reporting for ASP.NET Core - How to Use the SkiaSharp-Based DevExpress Drawing Engine

This example demonstrates how to use the DevExpress.Drawing package based on the [SkiaSharp](https://github.com/mono/SkiaSharp) library instead of System.Drawing library in an ASP.NET Core application to preview, [print](http://docs.devexpress.com/XtraReports/15797), or [export](http://docs.devexpress.com/XtraReports/2618) DevExpress XtraReports.

The commands required to configure the host operating system environment for the DevExpress Drawing Engine are included in the docker file.

## How to build and run this example

### Visual Studio

You can run the app on Windows platform, Windows Subsystem for Linux or Docker. Select a platform from the Debug drop-down in the toolbar, and start debugging the app.

### CLI
Run the application from the dotnet CLI on Windows, Linux and MacOS with the `dotnet run` command.
To run the Docker container from the command line, build the Docker image. You should pass the DevExpress NuGet source URL as a secret to restore NuGet packages. Review the [BuildKit documentation](https://docs.docker.com/build/buildkit/) for more information.

```console
set DX_NUGET=https://nuget.devexpress.com/some-nuget-token/api
docker build -t reporting-app --secret id=dxnuget,env=DX_NUGET .
docker run -p 8080:80 reporting-app:latest
```

```shell
export DX_NUGET=https://nuget.devexpress.com/some-nuget-token/api
DOCKER_BUILDKIT=1 docker build -t reporting-app --secret id=dxnuget,env=DX_NUGET .
docker run -p 8080:80 reporting-app:latest
```

The application page is available at the following URL: http://localhost:8080/.

## Files to look at

- [Startup.cs](ReportingWebApp/Startup.cs)

    At startup, call the `DevExpress.Drawing.Internal.DXDrawingEngine.ForceSkia` method to use the **DevExpress Drawing Skia** engine in the application.
- [ReportingWebApp.csproj](ReportingWebApp/ReportingWebApp.csproj)

    The `DockerfileFile` property in the project file specifies the name of the docker file to use in the project. The sample docker files for different OS are included in the project. You should edit the project file manually to replace the default **Debian** docker file with docker files for **Alpine**, **Ubuntu** or **Amazon Linux**. For more information on the build properties in a project file, review the following help topic: [Container Tools build properties](https://docs.microsoft.com/en-us/visualstudio/containers/container-msbuild-properties?view=vs-2022).
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

## More Examples

- [How to Use the DevExpress CrossPlatform Drawing Engine in an ASP.NET Core Application](https://github.com/DevExpress-Examples/Reporting-Use-the-DevExpress-CrossPlatform-Drawing-Engine)