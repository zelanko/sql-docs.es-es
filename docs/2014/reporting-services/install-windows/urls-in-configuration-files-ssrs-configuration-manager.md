---
title: Direcciones URL en archivos de configuración (Administrador de configuración de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- URL configuration [Reporting Services]
ms.assetid: 4f5e7fe0-b5b1-4665-93d4-80dce12d6b14
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c4df71d3110a878467c6dfd3a3281b4d597f2b7b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108591"
---
# <a name="urls-in-configuration-files--ssrs-configuration-manager"></a>Direcciones URL en archivos de configuración (Administrador de configuración de SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] almacena la configuración de las aplicaciones en un archivo RSReportServer.config. Dentro de este archivo, hay valores de configuración tanto de direcciones URL como de reservas de direcciones URL. Estos valores de configuración tienen propósitos muy diferentes y reglas de modificación. Si está acostumbrado a modificar los archivos de configuración para mejorar una implementación, este tema puede ayudarle a entender cómo se utiliza cada valor de las direcciones URL.  
  
## <a name="url-settings-in-rsreportserverconfig-file"></a>Configuración de direcciones URL en el archivo RSReportServer.config  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] almacena direcciones URL para el acceso a informes y aplicaciones, y para conectar los componentes web front-end a un servidor de informes back-end.  
  
#### <a name="urls-for-application-access"></a>Direcciones URL para el acceso de las aplicaciones  
 Las direcciones URL se usan para tener acceso al servicio web del servidor de informes y al Administrador de informes. Para configurar las direcciones URL, debe usar la herramienta Configuración de Reporting Services. La herramienta crea reservas de direcciones URL para cada aplicación en HTTP.SYS y agrega entradas para las direcciones URL en la sección `URLReservations` de RSReportServer.config.  
  
-   Para ver las descripciones de cada `URLReservations` elemento de la sección, vea archivo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de [configuración RSReportServer](../report-server/rsreportserver-config-configuration-file.md) en los libros en pantalla de.  
  
-   Para obtener más información sobre la sintaxis de solo `UrlString` el elemento, vea [Sintaxis de reserva de direcciones URL &#40;SSRS Configuration Manager&#41;](url-reservation-syntax-ssrs-configuration-manager.md).  
  
-   Para obtener instrucciones sobre cómo configurar las direcciones URL para el acceso a aplicaciones, vea [Configurar una dirección URL &#40;Administrador de configuración de SSRS&#41;](configure-a-url-ssrs-configuration-manager.md).  
  
#### <a name="urls-for-report-access"></a>Direcciones URL para el acceso de los informes  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] incluye una extensión de entrega de correo electrónico del servidor de informes que puede usar para enviar vínculos o datos adjuntos de informes. Un vínculo de informe se construye cuando se entrega el informe. La extensión de entrega de correo electrónico del servidor de informes usa el valor de `UrlRoot` del archivo de configuración para crear el vínculo. 
  `UrlRoot` se usa también para resolver los vínculos de un informe representado que se genera mediante el procesamiento de informes desatendido.  
  
 
  `UrlRoot` se especifica en el archivo RSReportServer.config automáticamente al configurar direcciones URL para el acceso de las aplicaciones. Si modifica este valor en el archivo de configuración, debe especificar una dirección URL válida para un servicio web del servidor de informes que esté conectado a una base de datos del servidor de informes que contenga los informes que desea entregar. Solo puede especificar una `UrlRoot` para una única instancia del servidor de informes; solo puede existir una entrada `UrlRoot` en el archivo RSReportServer.config para una instancia del servidor de informes determinada. Si tiene varias direcciones URL reservadas para el servicio web del servidor de informes, debe elegir uno de los valores disponibles de `UrlRoot`.  
  
 En la mayor parte de los casos, no necesita modificar `UrlRoot`. Sin embargo, si se va a tener acceso al servidor de informes a través de una dirección URL completa, y no configuró una dirección URL que use un encabezado de host para el nombre completo del sitio, debe editar el archivo RSReportServer `UrlRoot` . config manualmente para establecer en la dirección URL del servidor de informes completo que se usará para representar https://www.adventure-works.com/mywebapp/reportserver)el informe (por ejemplo,.  
  
#### <a name="urls-connecting-report-manager-and-web-parts-to-the-report-server-web-service"></a>Direcciones URL que conectan el Administrador de informes y los elementos web al servicio web del servidor de informes  
 El Administrador de informes y los elementos web de SharePoint 2.0 para Reporting Services son los componentes web front-end que conectan con un servidor de informes. Entre las direcciones URL que se usan para conectar con un servidor de informes back-end se incluyen las siguientes:  
  
-   
  `ReportServerUrl` (que usa el Administrador de informes)  
  
-   
  `ReportServerExternalUrl` (que usan los elementos web)  
  
> [!NOTE]  
>  Las versiones anteriores de Reporting Services incluían el elemento `ReportServerVirtualDirectory`. Este valor es obsoleto en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores. Si actualizó una instalación existente y usa un archivo de configuración que contiene este valor, el servidor de informes ya no lee este valor.  
  
 En la tabla siguiente se proporciona un resumen de todas las direcciones URL que se pueden especificar en un archivo de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
|Configuración|Uso|Descripción|  
|-------------|-----------|-----------------|  
|`ReportServerUrl`|Opcional. Este elemento no está incluido en el archivo RSReportServer.config a menos que lo agregue usted. Establezca este elemento solo si está configurando uno de los escenarios siguientes:<br /><br /> El Administrador de informes proporciona acceso web front-end a un servicio web del servidor de informes que se ejecuta en un equipo diferente o en una instancia diferente en el mismo equipo.<br /><br /> Tiene varias direcciones URL para un servidor de informes y desea que el Administrador de informes utilice una en concreto.<br /><br /> Tiene una dirección URL concreta del servidor de informes que desea que se use en todas las conexiones del Administrador de informes.<br /><br /> Por ejemplo, podría habilitar el acceso al Administrador de informes para todos los equipos de la red, y seguir requiriendo que el Administrador de informes se conecte al servidor de informes a través de una conexión local. En este caso, puede configurar `ReportServerUrl` en "http://localhost/reportserver".<br /><br /> <br /><br /> Para obtener instrucciones sobre cómo implementar estos escenarios, vea [configurar Administrador de informes &#40;modo nativo&#41;](../report-server/configure-web-portal.md) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los libros en pantalla de.|Este valor especifica una dirección URL para el servicio web del servidor de informes. La aplicación Administrador de informes lee este valor en el inicio. Si se establece este valor, el Administrador de informes se conectará al servidor de informes que se especifique en la dirección URL.<br /><br /> De forma predeterminada, el Administrador de informes proporciona acceso web front-end a un servicio web del servidor de informes que se ejecute dentro de la misma instancia del servidor de informes que él. Sin embargo, si desea utilizar el Administrador de informes con un servicio web del servidor de informes que forme parte de otra instancia o se ejecute en una instancia en un equipo diferente, puede establecer esta dirección URL para indicarle que se conecte al servicio web del servidor de informes externo.<br /><br /> Si en el servidor de informes al que se está conectando hay instalado un certificado de Capa de sockets seguros (SSL), el valor de `ReportServerUrl` debe ser el nombre del servidor que esté registrado para ese certificado. Si se produce un error similar a "Se ha terminado la conexión: no se puede establecer una relación de confianza para el canal seguro SSL/TLS", establezca `ReportServerUrl` en el nombre de dominio completo del servidor para el que se ha emitido el certificado SSL. Por ejemplo, si se ha registrado el certificado para **https:\//adventure-works.com.onlinesales**, la dirección URL del servidor de informes será **https:\//adventure-works.com.onlinesales/reportserver**.|  
|`ReportServerExternalUrl`|Opcional. Este elemento no está incluido en el archivo RSReportServer.config a menos que lo agregue usted.<br /><br /> Establezca este elemento solo si está utilizando los elementos web de SharePoint 2.0 y desea que los usuarios puedan recuperar un informe y abrirlo en otra ventana del explorador.<br /><br /> Agregue <`ReportServerExternalUrl`> debajo del elemento `ReportServerUrl` <> y, a continuación, establézcalo en un nombre de servidor de informes completo que se resuelva como una instancia del servidor de informes cuando se tenga acceso a ella en una ventana del explorador independiente. No elimine <`ReportServerUrl`>.<br /><br /> El siguiente ejemplo ilustra la sintaxis:<br /><br /> `<ReportServerExternalUrl>http://myserver/reportserver</ReportServerExternalUrl>`|Los elementos web de SharePoint 2.0 utilizan este valor.<br /><br /> En versiones anteriores, se recomendaba que estableciera este valor para implementar el Generador de informes en un servidor de informes expuesto a Internet. Este escenario de implementación no se ha probado. Si antes utilizaba este valor para que se admitiera el acceso a través de Internet al Generador de informes, debe considerar la posibilidad de utilizar una estrategia alternativa.|  
  
## <a name="see-also"></a>Consulte también  
 [Configurar las direcciones URL del servidor de informes &#40;Administrador de configuración de SSRS&#41;](configure-report-server-urls-ssrs-configuration-manager.md)   
 [Configurar una dirección URL &#40;Administrador de configuración de SSRS&#41;](configure-a-url-ssrs-configuration-manager.md)  
  
  
