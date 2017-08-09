---
title: "Introducción al control ReportViewer 2016 | Documentos de Microsoft"
ms.custom: 
ms.date: 06/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 01a821c4-2920-400c-be03-93d26c749bb1
caps.latest.revision: 12
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: a6a0bbee9141df565966df3e90f396e33c9b96a7
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="integrating-reporting-services-using-reportviewer-controls---get-started"></a>Integración de Reporting Services utilizando controles ReportViewer: empezar a trabajar

Obtenga información acerca de cómo los desarrolladores pueden incrustar informes paginados en sitios web de ASP.Net y aplicaciones de formularios de Windows, a través del Control de ReportViewer Reporting Services 2016. Puede agregar el control a un nuevo proyecto, o actualizar un proyecto existente.

## <a name="adding-the-reportviewer-control-to-a-new-web-project"></a>Agregar el control ReportViewer a un nuevo proyecto web

1. Crear un nuevo **sitio Web ASP.NET vacía** o abrir un proyecto ASP.NET existente.

    ![Crear-nueva-ASPNET-proyecto ssRS](../../reporting-services/application-integration/media/ssrs-create-new-aspnet-project.png)

2. Instalar el paquete de nuget del control ReportViewer 2016 a través de la **consola del Administrador de paquetes de Nuget**.

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WebForms
    ```
3. Agregar una nueva página .aspx al proyecto y registrar el ensamblado del control ReportViewer para su uso dentro de la página.

    ```
    <%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>
    ```
    
4. Agregar un **ScriptManagerControl** a la página.

5. Agregar el control ReportViewer a la página. El siguiente fragmento puede actualizarse para hacer referencia a un informe hospedado en un servidor de informes remoto.

    ```
    <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote">
      <ServerReport ReportPath="" ReportServerUrl="" />
    </rsweb:ReportViewer>
    ```
    
La página final debe ser similar al siguiente.

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="Sample" %>

<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <meta http-equiv="X-UA-Compatible" content="IE=edge" /> 
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
    <asp:ScriptManager runat="server"></asp:ScriptManager>        
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote">
            <ServerReport ReportServerUrl="http://AContosoDepartment/ReportServer" ReportPath="/LatestSales" />
        </rsweb:ReportViewer>
    </form>
</body>
</html>

```

## <a name="updating-an-existing-project-to-use-the-reportviewer-control"></a>Actualizar un proyecto existente para usar el control ReportViewer

Para hacer usar del control ReportViewer 2016 en un proyecto existente, agregue el control a través de Nuget y actualizar las referencias de ensamblado a la versión *14.0.0.0*. Esto incluirá la actualización de web.config del proyecto y todas las páginas .aspx que hace referencia al control ReportViewer.

### <a name="sample-webconfig-changes"></a>Cambios de web.config de ejemplo

```
<?xml version="1.0"?>
<!--
  For more information on how to configure your ASP.NET application, please visit
  http://go.microsoft.com/fwlink/?LinkId=169433
  -->
<configuration>
  <system.web>
    <compilation debug="true" targetFramework="4.5.2">
      <assemblies>
        <!-- All assemblies updated to version 14.0.0.0. -->
        <add assembly="Microsoft.ReportViewer.Common, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.DataVisualization, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.Design, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.ProcessingObjectModel, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WebDesign, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WinForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
      </assemblies>
      <buildProviders>
        <!-- Version updated to 14.0.0.0. -->
        <add extension=".rdlc"
          type="Microsoft.Reporting.RdlBuildProvider, Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
      </buildProviders>
    </compilation>
    <httpRuntime targetFramework="4.5.2"/>
    <httpHandlers>
      <!-- Version updated to 14.0.0.0 -->
      <add path="Reserved.ReportViewerWebControl.axd" verb="*"
        type="Microsoft.Reporting.WebForms.HttpHandler, Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"
        validate="false"/>
    </httpHandlers>
  </system.web>
  <system.webServer>
    <validation validateIntegratedModeConfiguration="false"/>
    <modules runAllManagedModulesForAllRequests="true"/>
    <handlers>
      <!-- Version updated to 14.0.0.0 -->
      <add name="ReportViewerWebControlHandler" verb="*" path="Reserved.ReportViewerWebControl.axd" preCondition="integratedMode"
        type="Microsoft.Reporting.WebForms.HttpHandler, Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
    </handlers>
  </system.webServer>
</configuration>
```

### <a name="sample-aspx"></a>Ejemplo .aspx

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="SampleAspx" %>

<!-- Update version to 14.0.0.0 -->
<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

<!DOCTYPE html>
```

## <a name="adding-the-reportviewer-control-to-a-new-windows-forms-project"></a>Agregar el control ReportViewer a un nuevo proyecto de Windows forms

1. Crear un nuevo **aplicación de Windows Forms** o abrir un proyecto existente.

    ![Crear-nueva-winforms-proyecto ssRS](../../reporting-services/application-integration/media/ssrs-create-new-winforms-project.png)

2. Instalar el paquete de nuget del control ReportViewer 2016 a través de la **consola del Administrador de paquetes de Nuget**.

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WinForms
    ```
3. Agregar un nuevo control desde el código o [agregar el control al cuadro de herramientas](##adding-control-to-visual-studio-toolbar).

    ```
    private Microsoft.Reporting.WinForms.ReportViewer reportViewer1;
    
    private void InitializeComponent()
    {
        this.reportViewer1 = new Microsoft.Reporting.WinForms.ReportViewer();
        this.SuspendLayout();
        // 
        // reportViewer1
        // 
        this.reportViewer1.Location = new System.Drawing.Point(168, 132);
        this.reportViewer1.Name = "reportViewer1";
        this.reportViewer1.ServerReport.BearerToken = null;
        this.reportViewer1.Size = new System.Drawing.Size(396, 246);
        this.reportViewer1.TabIndex = 0;
        // 
        // Form1
        // 
        this.Controls.Add(this.reportViewer1);
    }
    ```

## <a name="how-to-set-100-height-on-the-report-viewer-2016-control"></a>Cómo establecer el alto de 100% en el control de 2016 de Visor de informes

El nuevo control de 2016 de Visor de informes está optimizado para las páginas de modo de estándares de HTML5 y funciona en todos los exploradores modernos. En el pasado, con el control RVC anterior, al establecer la propiedad height de 100%, ha funcionado aunque ninguno de los antecesores tenía alto especificado. Este comportamiento ha cambiado en HTML5. Cuando se establece esta propiedad en el nuevo control RVC, funcionará correctamente sólo si el elemento primario tiene un alto definido, es decir, no un valor de "auto" o todos los antecesores de RVC tienen alto de 100% también.

A continuación se muestran los dos ejemplos de ello.

### <a name="by-setting-the-height-of-all-the-parent-elements-to-100"></a>Al establecer el alto de todas las principales de los elementos al 100%

```
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <style>
        html,body,form,#div1 {
            height: 100%; 
        }
    </style>
   </head>
<body>
    <form id="form1" runat="server">
    <div id="div1" >
            <asp:ScriptManager runat="server"></asp:ScriptManager>
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote" Height="100%" Width="100%">
            <ServerReport ReportServerUrl="http://test/ReportServer" ReportPath="/testreport" />
        </rsweb:ReportViewer>
    </div>
    </form>
</body>
</html>

```

### <a name="by-setting-the-style-height-attribute-on-the-parent-of-the-reportviewer-control"></a>Estableciendo el atributo height estilo en el elemento primario del control reportviewer

Para obtener más información acerca de longitudes de porcentaje del área de visualización, consulte [longitudes de porcentaje de la ventanilla](https://www.w3.org/TR/css3-values/#viewport-relative-lengths).

```
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
</head>
<body>
    <form id="form1" runat="server">
    <div style="height:100vh;">
            <asp:ScriptManager runat="server"></asp:ScriptManager>
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote" Height="100%" Width="100%">
            <ServerReport ReportServerUrl="http://test/ReportServer" ReportPath="/testreport" />
        </rsweb:ReportViewer>
    </div>
    </form>
</body>
</html>

```

## <a name="adding-control-to-visual-studio-toolbar"></a>Agregar control a la barra de herramientas de Visual Studio

El Control de Visor de informes ahora se incluye como un paquete de NuGet. Por este motivo, no verá el Control de Visor de informes aparecen en el cuadro de herramientas de Visual Studio de forma predeterminada. Puede agregar el control al cuadro de herramientas mediante los pasos siguientes.

1. Instale el paquete de NuGet para el formularios Windows Forms o formularios Web Forms, como se mencionó anteriormente.

2. Quitar el ReportViewer Control que se muestra en el cuadro de herramientas. Se trata el control con una versión de 12.x.

    ![ssRS-remove-antiguo-rvcontrol-cuadro de herramientas](../../reporting-services/application-integration/media/ssrs-remove-old-rvcontrol-toolbox.png)

3. Haga clic en cualquier lugar en el cuadro de herramientas y, a continuación, seleccione **elegir elementos... **.

    ![ssRS-cuadro de herramientas-elija-item](../../reporting-services/application-integration/media/ssrs-toolbox-choose-item.png)
    
4. En el **componentes de .NET Framework**, seleccione **examinar**.

    ![exploración de cuadro de herramientas de ssRS](../../reporting-services/application-integration/media/ssrs-toolbox-browse.png)

5. Seleccione el **Microsoft.ReportViewer.WinForms.dll** o **Microsoft.ReportViewer.WebForms.dll** desde el paquete de NuGet que se ha instalado.

    > [!NOTE] 
    > El paquete de NuGet se instalará en el directorio de la solución del proyecto. La ruta de acceso al archivo dll será similar al siguiente: `{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.Winforms.{version}\lib\net40` o `{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.WebForms.{version}\lib\net40`.

6. El nuevo control debe mostrarse en el cuadro de herramientas. A continuación, puede moverlo a otra ficha en el cuadro de herramientas si lo desea.

    ![rvcontrol de cuadro de herramientas de ssRS](../../reporting-services/application-integration/media/ssrs-toolbox-rvcontrol.png)

### <a name="things-to-be-aware-of"></a>Cosas a tener en cuenta

- Esto agregará una referencia al paquete de NuGet instalado dentro del proyecto actual. El elemento en el cuadro de herramientas se conservará a otros proyectos. Cuando se instala el paquete de NuGet en una nueva solución o proyecto, el elemento de cuadro de herramientas puede hacer referencia a una versión anterior. 

- Incluso si el ensamblado ya no está disponible, el control permanecerá en el cuadro de herramientas. Si se ha eliminado ese proyecto, Visual Studio se producirá un error si intenta agregar el control del cuadro de herramientas. Para corregir este error, quite el control del cuadro de herramientas y vuelva a agregarlo siguiendo los pasos anteriores.


## <a name="common-issues"></a>Problemas comunes
    
- El control ReportViewer 2016 está diseñado para utilizarse con los exploradores modernos. El control podría no funcionar si los exploradores representar la página web en un modo de compatibilidad de Internet Explorer. Sitios de intranet pueden requerir una etiqueta meta para invalidar la configuración que fomentar la representación de páginas en modo de compatibilidad de la intranet.

    ```
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    ```
      
## <a name="providing-feedback"></a>Proporcionar comentarios

Informar al equipo acerca de los problemas que pueda surgir con el control en el [foros de MSDN de servicios de informes](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlreportingservices) o a través de correo electrónico en [ RVCFeedback@microsoft.com ](mailto:RVCFeedback@microsoft.com).

## <a name="see-also"></a>Vea también

[Recopilación de datos en el control de ReportingViewer de 2016](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls-data-collection.md)  
¿Más preguntas? [Pruebe el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)


