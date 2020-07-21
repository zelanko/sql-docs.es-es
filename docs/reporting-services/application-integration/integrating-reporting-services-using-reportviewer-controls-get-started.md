---
title: Introducción a los controles del Visor de informes
description: Los controles de Visor de informes sirven para integrar informes RDL de Reporting Services en aplicaciones WebForms y WinForms.
ms.custom: seo-lt-2019
ms.date: 12/12/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: conceptual
ms.assetid: 01a821c4-2920-400c-be03-93d26c749bb1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d7e1e64bddcdcc7efed701770aea0e97c8e84ec5
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "75241825"
---
# <a name="integrating-reporting-services-using-the-report-viewer-controls---get-started"></a>Integración de Reporting Services con los controles del Visor de informes: Introducción

Los controles de Visor de informes sirven para integrar informes RDL de Reporting Services en aplicaciones WebForms y WinForms. Para saber más sobre las actualizaciones recientes, vea el [registro de cambios](changelog.md).

## <a name="adding-the-report-viewer-control-to-a-new-web-project"></a>Agregar el control del Visor de informes a un nuevo proyecto web

1. Cree un **sitio web vacío de ASP.NET** o abra un proyecto de ASP.NET existente.

    ![ssRS-Create-New-ASPNET-Project](../../reporting-services/application-integration/media/ssrs-create-new-aspnet-project.png)

2. Instale el paquete de NuGet del control del Visor de informes mediante la **consola del administrador de paquetes de NuGet**.

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WebForms
    ```
3. Agregue una nueva página .aspx al proyecto y registre el ensamblado del control del Visor de informes para usarlo en la página.

    ```
    <%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>
    ```
    
4. Agregue un **ScriptManagerControl** a la página.

5. Agregue el control del Visor de informes a la página. El siguiente fragmento de código se puede actualizar para hacer referencia a un informe hospedado en un servidor de informes remoto.

    ```
    <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote">
      <ServerReport ReportPath="" ReportServerUrl="" />
    </rsweb:ReportViewer>
    ```
    
La página final debería ser similar a la siguiente.

```html
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="Sample" %>

<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

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
            <ServerReport ReportServerUrl="https://AContosoDepartment/ReportServer" ReportPath="/LatestSales" />
        </rsweb:ReportViewer>
    </form>
</body>
</html>
```

## <a name="updating-an-existing-project-to-use-the-report-viewer-control"></a>Actualizar un proyecto existente para usar el control del Visor de informes

Asegúrese de actualizar todas las referencias de ensamblado a la versión *15.0.0.0*, incluidas las páginas web.config del proyecto y todas las páginas .aspx que hacen referencia al control del visor.

### <a name="sample-webconfig-changes"></a>Cambios del archivo web.config de ejemplo

```xml
<?xml version="1.0"?>
<!--
  For more information on how to configure your ASP.NET application, please visit
  https://go.microsoft.com/fwlink/?LinkId=169433
  -->
<configuration>
  <system.web>
    <compilation debug="true" targetFramework="4.5.2">
      <assemblies>
        <!-- All assemblies updated to version 15.0.0.0. -->
        <add assembly="Microsoft.ReportViewer.Common, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.DataVisualization, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.Design, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.ProcessingObjectModel, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WebDesign, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WinForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
      </assemblies>
      <buildProviders>
        <!-- Version updated to 15.0.0.0. -->
        <add extension=".rdlc"
          type="Microsoft.Reporting.RdlBuildProvider, Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
      </buildProviders>
    </compilation>
    <httpRuntime targetFramework="4.5.2"/>
    <httpHandlers>
      <!-- Version updated to 15.0.0.0 -->
      <add path="Reserved.ReportViewerWebControl.axd" verb="*"
        type="Microsoft.Reporting.WebForms.HttpHandler, Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"
        validate="false"/>
    </httpHandlers>
  </system.web>
  <system.webServer>
    <validation validateIntegratedModeConfiguration="false"/>
    <modules runAllManagedModulesForAllRequests="true"/>
    <handlers>
      <!-- Version updated to 15.0.0.0 -->
      <add name="ReportViewerWebControlHandler" verb="*" path="Reserved.ReportViewerWebControl.axd" preCondition="integratedMode"
        type="Microsoft.Reporting.WebForms.HttpHandler, Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
    </handlers>
  </system.webServer>
</configuration>
```

### <a name="sample-aspx"></a>Páginas .aspx de ejemplo

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="SampleAspx" %>

<!-- Update version to 15.0.0.0 -->
<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

<!DOCTYPE html>
```

## <a name="adding-the-report-viewer-control-to-a-new-windows-forms-project"></a>Agregar el control del Visor de informes a un proyecto nuevo de Windows Forms

1. Cree una **aplicación de Windows Forms** o abra un proyecto existente.

    ![ssRS-Create-New-winforms-Project](../../reporting-services/application-integration/media/ssrs-create-new-winforms-project.png)

2. Instale el paquete de NuGet del control del Visor de informes mediante la **consola del administrador de paquetes de NuGet**.

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WinForms
    ```
3. Agregue un nuevo control desde el código o [agregue el control al cuadro de herramientas](#adding-control-to-visual-studio-toolbar).

    ```csharp
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

## <a name="how-to-set-100-height-on-the-report-viewer-control"></a>Configurar el alto en 100 % en el control del Visor de informes

Si se establece el alto del control del visor en 100 %, el elemento primario deberá tener un alto definido, o todos los antecesores tendrán que tener altos de porcentaje.

### <a name="setting-the-height-of-all-the-ancestors-to-100"></a>Configurar el alto de todos los antecesores en 100 %

```html
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
            <ServerReport ReportServerUrl="https://test/ReportServer" ReportPath="/testreport" />
        </rsweb:ReportViewer>
    </div>
    </form>
</body>
</html>
```

### <a name="setting-the-parents-height-attribute"></a>Configurar el atributo de alto del elemento primario

Para más información sobre las longitudes porcentuales de la ventanilla, vea [Viewport-percentage lengths](http://www.w3.org/TR/css3-values/#viewport-relative-lengths) (Longitudes porcentuales de la ventanilla).

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
</head>
<body>
    <form id="form1" runat="server">
    <div style="height:100vh;">
            <asp:ScriptManager runat="server"></asp:ScriptManager>
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote" Height="100%" Width="100%">
            <ServerReport ReportServerUrl="https://test/ReportServer" ReportPath="/testreport" />
        </rsweb:ReportViewer>
    </div>
    </form>
</body>
</html>
```

## <a name="adding-control-to-visual-studio-toolbar"></a>Agregar control a la barra de herramientas de Visual Studio

El control del Visor de informes ahora se distribuye como un paquete de NuGet y ya no se muestra en el cuadro de herramientas de Visual Studio de forma predeterminada. Puede agregar manualmente el control al cuadro de herramientas.

1. Instale el paquete de NuGet para WinForms o WebForms, como se indica más arriba.

2. Quite el control del Visor de informes que aparece en el cuadro de herramientas.

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

## <a name="common-issues"></a>Problemas comunes
    
El control de visor está diseñado para los exploradores modernos. Puede que el control no funcione según lo esperado si el explorador representa la página mediante el modo de compatibilidad de IE. Es posible que los sitios de intranet necesiten una metaetiqueta para invalidar el comportamiento predeterminado del explorador.

    ```
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    ```
      
## <a name="feedback"></a>Comentarios

Avise al equipo de cualquier problema a través de los [foros de Reporting Services](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlreportingservices).

## <a name="see-also"></a>Consulte también

[Recopilación de datos en el control del Visor de informes](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls-data-collection.md)  
¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).

