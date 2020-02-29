---
title: Cambiar la extensión de entrega predeterminada de Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Manager [Reporting Services], default delivery extension
ms.assetid: 5f6fee72-01bf-4f6c-85d2-7863c46c136b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2a92d967e0b37f1143c9fd37a0d5ee8154ac21db
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/28/2020
ms.locfileid: "78177125"
---
# <a name="change-the-default-reporting-services-delivery-extension"></a>Cambiar la extensión de entrega predeterminada de Reporting Services
  Puede modificar las opciones de configuración de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] para cambiar la extensión de entrega predeterminada que aparece en la lista **Entregado por** de una página de definición de suscripción. Por ejemplo, puede modificar la configuración de modo que cuando los usuarios creen una nueva suscripción, la entrega de recurso compartido de archivos se seleccione de forma predeterminada en lugar de la entrega por correo electrónico. También puede cambiar el orden en que se muestran las extensiones de entrega en la interfaz de usuario.

 **[!INCLUDE[applies](../../includes/applies-md.md)]** Modo nativo de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] | Modo de SharePoint de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]

 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] incluye las extensiones de entrega Correo electrónico y Recurso compartido de archivos de Windows. El servidor de informes puede tener extensiones de entrega adicionales si ha implementado extensiones personalizadas o de otros fabricantes para admitir la entrega personalizada. La disponibilidad de una extensión de entrega depende de si está implementada en un servidor de informes.

## <a name="default-native-mode-report-server-configuration"></a>Configuración predeterminada del servidor de informes de modo nativo
 El orden en el que una extensión de entrega aparece en el Administrador de informes en la lista **Entregado por** se basa en el orden de las entradas de extensión de entrega del archivo **RSReportServer.config** . Por ejemplo, la siguiente imagen muestra el correo electrónico primero en la lista y está seleccionado de forma predeterminada.

 ![lista predeterminada de extensiones de entrega](../media/ssrs-default-delivery.png "lista predeterminada de extensiones de entrega")

 La siguiente es la sección predeterminada de **RSReportServer.config** que controla la extensión de entrega predeterminada y el orden en que se muestran en el Administrador de informes. Tenga en cuenta que el correo electrónico aparece en primer lugar en el archivo y se establece como valor predeterminado.

```xml
<DeliveryUI>
     <Extension Name="Report Server Email" Type="Microsoft.ReportingServices.EmailDeliveryProvider.EmailDeliveryProviderControl,ReportingServicesEmailDeliveryProvider">
          <DefaultDeliveryExtension>True</DefaultDeliveryExtension>
               <Configuration>
               <RSEmailDPConfiguration>
                    <DefaultRenderingExtension>MHTML</DefaultRenderingExtension>
               </RSEmailDPConfiguration>
               </Configuration>
     </Extension>
     <Extension Name="Report Server FileShare" Type="Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareUIControl,ReportingServicesFileShareDeliveryProvider"/>
</DeliveryUI>
```

#### <a name="configure-file-share-delivery-as-the-default-delivery-extension-in-report-manager"></a>Configure la entrega de recurso compartido de archivos como la extensión de entrega predeterminada en el Administrador de informes

1.  Los pasos de este procedimiento modifican la configuración para que la entrega de recurso compartido aparece como la primera opción en la interfaz de usuario y es la selección predeterminada.

     Abra el archivo RSReportServer.config en un editor de texto. Para obtener más información acerca del archivo de configuración, consulte [RSReportServer Configuration File](../report-server/rsreportserver-config-configuration-file.md). Después de que cambie la configuración, la interfaz de usuario será similar a la siguiente imagen:

     ![lista de extensiones de entrega modificada](../media/ssrs-modified-delivery.png "lista de extensiones de entrega modificada")

2.  Modifique la sección DeliveryUI para que el aspecto sea como en el ejemplo siguiente y tenga en cuenta los cambios clave de:

    1.  La extensión de recurso compartido de archivos está antes de la extensión de correo electrónico. Esto cambiará el orden en que las extensiones aparecen en el Administrador de informes.

    2.  La extensión de recurso compartido de archivos contiene la etiqueta DefaultExtension `<DefaultDeliveryExtension>True</DefaultDeliveryExtension>` y se agregó la etiqueta de cierre de extensión `</Extension>`.

    3.  La extensión de correo electrónico ya no está configurada como el valor predeterminado. `<DefaultDeliveryExtension>False</DefaultDeliveryExtension>`

    ```
    <DeliveryUI>
         <Extension Name="Report Server FileShare" Type="Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareUIControl,ReportingServicesFileShareDeliveryProvider">
              <DefaultDeliveryExtension>True</DefaultDeliveryExtension>
         </Extension>
         <Extension Name="Report Server Email" Type="Microsoft.ReportingServices.EmailDeliveryProvider.EmailDeliveryProviderControl,ReportingServicesEmailDeliveryProvider">
         <DefaultDeliveryExtension>False</DefaultDeliveryExtension>
         <Configuration>
              <RSEmailDPConfiguration>
                   <DefaultRenderingExtension>MHTML</DefaultRenderingExtension>
              </RSEmailDPConfiguration>
         </Configuration>
         </Extension>
    </DeliveryUI>
    ```

3.  Guarde el archivo de configuración.

4.  En pocos minutos el servidor de informes volverá a cargar el archivo de configuración y la nueva configuración surtirá efecto. Puede reiniciar el servicio del servidor de informes para forzar la carga del archivo de configuración.

     Cuando se lee la configuración, se escribe el siguiente evento en el registro de eventos de Windows.

     **Id. de evento**: 109

     **Origen**: Servicio Servidor de informes de Windows (nombre de instancia)

     Se ha modificado el archivo RSReportServer.config

## <a name="sharepoint-mode-report-servers"></a>Servidores de informes en modo de SharePoint
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] El modo de SharePoint almacena la información de las extensiones en las bases de datos de aplicación de servicio de SharePoint y no en el archivo RsrReportServer.config. En el modo de SharePoint, la configuración de la extensión de entrega se modifica con PowerShell.

#### <a name="configure-the-default-delivery-extension"></a>Configurar la extensión de entrega predeterminada

1.  Abra el **Shell de administración de SharePoint**.

2.  Puede omitir este paso si ya conoce el nombre de su aplicación de servicio de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] . Use el PowerShell siguiente a la lista de las aplicaciones de servicio de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] en la granja de SharePoint.

    ```powershell
    Get-SPRSServiceApplication | Format-List *
    ```

3.  Ejecute el PowerShell siguiente para comprobar la extensión de entrega predeterminada actual para la aplicación de servicio "ssrsapp" de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].

    ```powershell
    $app = Get-SPRSServiceApplication | Where {$_.name -Like "ssrsapp*"};
    Get-SPRSExtension -Identity $app | Where {$_.ServerDirectivesXML -Like "<DefaultDelivery*"} | Format-List *
    ```

## <a name="see-also"></a>Consulte también
 [Archivo de configuración](../report-server/rsreportserver-config-configuration-file.md) RSReportServer [distribución del recurso compartido de archivos de configuración del archivo de configuración en Reporting Services](file-share-delivery-in-reporting-services.md) [entrega de correo electrónico en Reporting Services](e-mail-delivery-in-reporting-services.md) [configurar un servidor de informes para la entrega de correo electrónico &#40;SSRS Configuration Manager&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md) [](../report-server/rsreportserver-config-configuration-file.md)
