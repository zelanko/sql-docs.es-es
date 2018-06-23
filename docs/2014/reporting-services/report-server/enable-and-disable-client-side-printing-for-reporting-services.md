---
title: Habilitar y deshabilitar la impresión del lado cliente para Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0e709c96-7517-4547-8ef6-5632f8118524
caps.latest.revision: 7
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 9b5c7c1d879b2ffc9cb333bed193af9239996536
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198605"
---
# <a name="enable-and-disable-client-side-printing-for-reporting-services"></a>Habilitar y deshabilitar la impresión del lado cliente para Reporting Services
  El [!INCLUDE[msCoName](../../includes/msconame-md.md)] control ActiveX, **RSClientPrint**, proporciona la impresión del lado cliente para los informes que se ve en un explorador. El control muestra un cuadro de diálogo personalizado de impresión que admite características comunes a otros cuadros de diálogo de impresión. Entre estas características se incluyen vista previa de impresión, selecciones de página para especificar páginas e intervalos específicos, márgenes de página y orientación. Aunque la impresión del lado cliente está habilitada de manera predeterminada, puede deshabilitar esta característica para impedir que sea utilizada.  
  
> [!NOTE]  
>  Para descargar controles ActiveX se requieren permisos de administrador.  
  
## <a name="downloading-the-activex-control"></a>Descargar el control ActiveX  
 Cada usuario que desee utilizar la función de impresión debe descargar e instalar el control ActiveX que ofrece la funcionalidad de impresión del lado cliente. La primera vez que un usuario hace clic en el **impresora** icono en la barra de herramientas de informe, el control se descarga en el equipo de Microsoft ActiveX. Una vez descargado el control, el **impresión** cuadro de diálogo muestra cada vez que el usuario hace clic en el **impresora** icono.  
  
 En función de la configuración del explorador, es posible que al usuario se le solicite instalar el control, se le impida instalar el control o se le obligue a instalar el control de un modo transparente en segundo plano.  
  
 Para [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer, la configuración que afectan a la instalación y la descarga del control ActiveX se especifica a través de la **ActiveX controles y complementos** nodo en el **configuración de seguridad** página la zona de contenido Web. La siguiente configuración determina si los usuarios pueden descargar y ejecutar el control de impresión en función de las preferencias de seguridad de la zona web:  
  
-   Descargar los controles ActiveX firmados.  
  
-   Activar script de los controles de ActiveX marcados como seguros.  
  
-   Ejecutar los controles y complementos para ActiveX.  
  
 Los usuarios que quieran usar **RSClientPrint** para realizar la impresión del lado cliente debe habilitar lo siguiente:  
  
-   **Descargar controles ActiveX firmados** y **control de Script ActiveX marcados como seguro para scripting** para realizar la instalación.  
  
-   **Ejecutar controles ActiveX y complementos** para las operaciones de impresión en curso.  
  
 El **RSClientPrint** control ActiveX está firmado, lo que significa contiene un certificado digital válido de [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
## <a name="enabling-and-disabling-client-side-printing"></a>Habilitar y deshabilitar la impresión de cliente  
 Los administradores del servidor de informes tienen la opción de deshabilitar la característica de impresión estableciendo la propiedad del sistema de servidor de informes **EnableClientPrinting** a `false`. De este modo se deshabilitará la impresión del lado cliente para todos los informes administrados por ese servidor. De forma predeterminada, **EnableClientPrinting** está establecido en `true`. Puede deshabilitar la impresión del lado cliente de las siguientes maneras:  
  
-   Para un **servidor de informes en modo nativo**:  
  
    1.  Inicie [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] con privilegios de administrador.  
  
    2.  Conéctese a una instancia del servidor de informes en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
    3.  Haga clic con el botón derecho en el nodo del servidor de informes y, después, haga clic en **Propiedades**. Si la opción **Propiedades** está deshabilitada, compruebe que inició [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] con privilegios de administrador.  
  
    4.  Seleccione **Habilitar descarga para el control de impresión de ActiveX client**.  
  
    5.  Haga clic en **Aceptar**.  
  
-   Para un **servidor de informes en modo de SharePoint**:  
  
    1.  En Administración central de SharePoint, haga clic en **Administración de aplicaciones**.  
  
    2.  Haga clic en **Administrar aplicaciones de servicio**.  
  
    3.  Haga clic el nombre de la aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y, a continuación, haga clic en **Administrar** en la cinta de opciones de SharePoint.  
  
    4.  Haga clic en **Configuración del sistema**.  
  
    5.  Seleccione **Habilitar la impresión de cliente**. La opción **Habilitar la impresión de cliente** está cerca de la parte inferior de la página.  
  
    6.  Haga clic en **Aceptar**.  
  
-   Escriba código para establecer la propiedad del sistema de servidor de informes o script **EnableClientPrinting** a `false.`  
  
 El siguiente script de ejemplo ilustra un enfoque válido para deshabilitar la impresión de lado cliente. Compile y ejecute el siguiente código de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] para establecer la propiedad **EnableClientPrinting** en **False**. Después de ejecutar el código, reinicie IIS.  
  
### <a name="sample-script"></a>Script de ejemplo  
  
```  
Imports System  
Imports System.Web.Services.Protocols  
Class Sample  
   Public Shared Sub Main()  
Dim rs As New ReportingService()  
      rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
        Dim props(0) As [Property]  
        Dim setProp As New [Property]  
        setProp.Name = "EnableClientPrinting"  
        setProp.Value = “False”   
        props(0) = setProp  
        Try  
            rs.SetSystemProperties(props)  
        Catch ex As System.Web.Services.Protocols.SoapException  
            Console.Write(ex.Detail.InnerXml)  
        Catch e as Exception  
            Console.Write(e.Message)  
        End Try  
    End Sub 'Main  
End Class 'Sample  
```  
  
  