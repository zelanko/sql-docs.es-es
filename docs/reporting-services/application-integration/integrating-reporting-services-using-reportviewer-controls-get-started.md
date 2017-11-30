---
title: "Introducción al control ReportViewer 2016 | Microsoft Docs"
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
caps.latest.revision: "12"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Active
ms.openlocfilehash: dff598efce33f778359c2b6fb4c3a0184f2b88f6
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="integrating-reporting-services-using-reportviewer-controls---get-started"></a>Integración de Reporting Services con los controles ReportViewer: introducción

Obtenga información sobre cómo pueden incrustar los desarrolladores informes paginados en sitios web de ASP.NET y aplicaciones de Windows Forms mediante el control ReportViewer de Reporting Services 2016. Puede agregar el control a un proyecto nuevo o actualizar un proyecto existente.

## <a name="adding-the-reportviewer-control-to-a-new-web-project"></a>Agregar el control ReportViewer a un nuevo proyecto web

1. Cree un **sitio web vacío de ASP.NET** o abra un proyecto de ASP.NET existente.

    ![ssRS-Create-New-ASPNET-Project](../../reporting-services/application-integration/media/ssrs-create-new-aspnet-project.png)

2. Instale el paquete de NuGet del control ReportViewer 2016 mediante la **consola del administrador de paquetes de NuGet**.

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WebForms
    ```
3. Agregue una nueva página .aspx al proyecto y registre el ensamblado del control ReportViewer para usarlo en la página.

    ```
    <%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>
    ```
    
4. Agregue un **ScriptManagerControl** a la página.

5. Agregue el control ReportViewer a la página. El siguiente fragmento de código se puede actualizar para hacer referencia a un informe hospedado en un servidor de informes remoto.

    ```
    <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote">
      <ServerReport ReportPath="" ReportServerUrl="" />
    </rsweb:ReportViewer>
    ```
    
La página final debería ser similar a la siguiente.

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

Para usar el control ReportViewer 2016 en un proyecto existente, agregue el control mediante NuGet y actualice las referencias del ensamblado a la versión *14.0.0.0*. Se incluye la actualización del archivo web.config del proyecto y todas las páginas .aspx que hacen referencia al control ReportViewer.

### <a name="sample-webconfig-changes"></a>Cambios del archivo web.config de ejemplo

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

### <a name="sample-aspx"></a>Páginas .aspx de ejemplo

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="SampleAspx" %>

<!-- Update version to 14.0.0.0 -->
<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

<!DOCTYPE html>
```

## <a name="adding-the-reportviewer-control-to-a-new-windows-forms-project"></a>Agregar el control ReportViewer a un proyecto nuevo de Windows Forms

1. Cree una **aplicación de Windows Forms** o abra un proyecto existente.

    ![ssRS-Create-New-winforms-Project](../../reporting-services/application-integration/media/ssrs-create-new-winforms-project.png)

2. Instale el paquete de NuGet del control ReportViewer 2016 mediante la **consola del administrador de paquetes de NuGet**.

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WinForms
    ```
3. Agregue un nuevo control desde el código o [agregue el control al cuadro de herramientas](##adding-control-to-visual-studio-toolbar).

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

## <a name="how-to-set-100-height-on-the-report-viewer-2016-control"></a>Cómo establecer la altura al 100% en el control de Visor de informes 2016

El nuevo control de Visor de informes 2016 está optimizado para las páginas en modo estándar HTML5 y funciona en todos los exploradores modernos. En el pasado, con el control RVC anterior, al establecer la propiedad de la altura al 100%, funcionaba aunque ninguno de los antecesores tuviera especificada la altura, pero este comportamiento ha cambiado en HTML5. Al establecer esta propiedad en el nuevo control RVC, funcionará correctamente solo si el elemento principal tiene una altura definida (es decir, que no tenga el valor "auto") o si todos los antecesores de RVC también tienen una altura del 100%.

A continuación se muestran los dos ejemplos para hacerlo.

### <a name="by-setting-the-height-of-all-the-parent-elements-to-100"></a>Estableciendo la altura de todos los elementos principales al 100%

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

### <a name="by-setting-the-style-height-attribute-on-the-parent-of-the-reportviewer-control"></a>Estableciendo el atributo height de estilo en el elemento primario del control reportviewer

Para más información sobre las longitudes porcentuales de la ventanilla, vea [Viewport-percentage lengths](https://www.w3.org/TR/css3-values/#viewport-relative-lengths) (Longitudes porcentuales de la ventanilla).

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

El control Visor de informes ahora se incluye como paquete de NuGet. Por este motivo, de forma predeterminada no verá aparecer el control Visor de informes en el cuadro de herramientas de Visual Studio. Puede agregar el control al cuadro de herramientas siguiendo estos pasos.

1. Instale el paquete de NuGet para WinForms o WebForms, como se indica más arriba.

2. Quite el control ReportViewer que aparece en el cuadro de herramientas. Se trata del control que tiene la versión 12.x.

    ![ssRS-remove-old-rvcontrol-toolbox](../../reporting-services/application-integration/media/ssrs-remove-old-rvcontrol-toolbox.png)

3. Haga clic con el botón derecho en cualquier lugar del cuadro de herramientas y seleccione **Elegir elementos…**

    ![ssRS-toolbox-choose-item](../../reporting-services/application-integration/media/ssrs-toolbox-choose-item.png)
    
4. En **Componentes de .NET Framework**, seleccione **Examinar**.

    ![ssRS-toolbox-browse](../../reporting-services/application-integration/media/ssrs-toolbox-browse.png)

5. Seleccione el archivo **Microsoft.ReportViewer.WinForms.dll** o **Microsoft.ReportViewer.WebForms.dll** en el paquete de NuGet instalado.

    > [!NOTE] 
    > El paquete de NuGet se instalará en el directorio de la solución del proyecto. La ruta de acceso al archivo dll será similar a la siguiente: `{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.Winforms.{version}\lib\net40` o `{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.WebForms.{version}\lib\net40`.

6. El nuevo control debe aparecer en el cuadro de herramientas. Luego, si quiere, podrá moverlo a otra pestaña del cuadro de herramientas.

    ![ssRS-toolbox-rvcontrol](../../reporting-services/application-integration/media/ssrs-toolbox-rvcontrol.png)

### <a name="things-to-be-aware-of"></a>Aspectos que debe tener en cuenta

- Se agregará una referencia al paquete de NuGet instalado dentro del proyecto actual. El elemento del cuadro de herramientas se conservará en otros proyectos. Al instalar el paquete de NuGet en una solución o proyecto nuevo, es posible que el elemento del cuadro de herramientas haga referencia a una versión anterior. 

- Incluso si el ensamblado ya no está disponible, el control permanecerá en el cuadro de herramientas. Si se ha eliminado ese proyecto, Visual Studio generará un error si intenta agregar el control desde el cuadro de herramientas. Para corregir este error, quite el control del cuadro de herramientas y vuelva a agregarlo siguiendo los pasos anteriores.


## <a name="common-issues"></a>Problemas comunes
    
- El control ReportViewer 2016 está diseñado para usarlo con exploradores modernos. El control podría no funcionar si los exploradores representan la página web en un modo de compatibilidad de Internet Explorer. Los sitios de intranet podrían necesitar una metaetiqueta para invalidar la configuración, que fomenta la representación de páginas de intranet en el modo de compatibilidad.

    ```
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    ```
      
## <a name="providing-feedback"></a>Envío de comentarios

Informe al equipo acerca de cualquier problema que pueda surgir con el control en los [foros de MSDN de Reporting Services](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlreportingservices) o por correo electrónico en [RVCFeedback@microsoft.com](mailto:RVCFeedback@microsoft.com).

## <a name="see-also"></a>Vea también

[Recopilación de datos en el control ReportingViewer 2016](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls-data-collection.md)  
¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).

