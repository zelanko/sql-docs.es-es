---
title: Habilitar y deshabilitar la impresión del lado cliente para Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 0e709c96-7517-4547-8ef6-5632f8118524
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ea5016aa51a25bd296d2e77516b30b84a7a28cec
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66103931"
---
# <a name="enable-and-disable-client-side-printing-for-reporting-services"></a>Habilitar y deshabilitar la impresión del lado cliente para Reporting Services
  El [!INCLUDE[msCoName](../../includes/msconame-md.md)] control ActiveX, **RSClientPrint**, proporciona la impresión del lado cliente para los informes que se ven en un explorador. El control muestra un cuadro de diálogo personalizado de impresión que admite características comunes a otros cuadros de diálogo de impresión. Entre estas características se incluyen vista previa de impresión, selecciones de página para especificar páginas e intervalos específicos, márgenes de página y orientación. Aunque la impresión del lado cliente está habilitada de manera predeterminada, puede deshabilitar esta característica para impedir que sea utilizada.  
  
> [!NOTE]  
>  Para descargar controles ActiveX se requieren permisos de administrador.  
  
## <a name="downloading-the-activex-control"></a>Descargar el control ActiveX  
 Cada usuario que desee utilizar la función de impresión debe descargar e instalar el control ActiveX que ofrece la funcionalidad de impresión del lado cliente. La primera vez que un usuario haga clic en el icono de la **impresora** en la barra de herramientas de informe, el control ActiveX de Microsoft se descargará en el equipo. Una vez descargado el control, el cuadro de diálogo **Imprimir** aparece siempre que el usuario hace clic en el icono de la **impresora** .  
  
 En función de la configuración del explorador, es posible que al usuario se le solicite instalar el control, se le impida instalar el control o se le obligue a instalar el control de un modo transparente en segundo plano.  
  
 En [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer, la configuración que afecta a la descarga e instalación del control ActiveX se especifica a través del nodo **controles y** complementos de ActiveX de la página **configuración de seguridad** de la zona de contenido Web. La siguiente configuración determina si los usuarios pueden descargar y ejecutar el control de impresión en función de las preferencias de seguridad de la zona web:  
  
-   Descargar los controles ActiveX firmados.  
  
-   Activar script de los controles de ActiveX marcados como seguros.  
  
-   Ejecutar los controles y complementos para ActiveX.  
  
 Los usuarios que deseen usar **RSClientPrint** para realizar la impresión del lado cliente deben habilitar lo siguiente:  
  
-   **Descargar controles ActiveX firmados** y **crear scripts de control ActiveX marcados como seguros para el scripting** con fines de instalación.  
  
-   **Ejecutar controles y complementos de ActiveX** para las operaciones de impresión en curso.  
  
 El control ActiveX **RSClientPrint** está firmado, lo que significa que contiene un certificado digital [!INCLUDE[msCoName](../../includes/msconame-md.md)]válido de.  
  
## <a name="enabling-and-disabling-client-side-printing"></a>Habilitar y deshabilitar la impresión de cliente  
 Los administradores del servidor de informes tienen la opción de deshabilitar la característica de impresión estableciendo la propiedad del **EnableClientPrinting** sistema del `false`servidor de informes EnableClientPrinting en. De este modo se deshabilitará la impresión del lado cliente para todos los informes administrados por ese servidor. De forma predeterminada, **EnableClientPrinting** se establece `true`en. Puede deshabilitar la impresión del lado cliente de las siguientes maneras:  
  
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
  
-   Escriba el script o el código para establecer la propiedad del sistema del servidor de informes **EnableClientPrinting** en`false.`  
  
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
        setProp.Value = "False"   
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
  
  
