---
title: Solución de problemas de suscripciones y entrega de Reporting Services
description: En este artículo, diagnosticará y solucionará los problemas encontrados al trabajar con suscripciones de informes, programaciones y entregas en SQL Server Reporting Services.
ms.date: 05/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
ms.assetid: ae1775f7-9919-48ca-8bd7-cc16df274e2c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 577ca01b2764df923c0208934c597e17e8412ff2
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2020
ms.locfileid: "80662751"
---
# <a name="troubleshoot-reporting-services-subscriptions-and-delivery"></a>Solución de problemas de suscripciones y entrega de Reporting Services
  
    
Use este tema para solucionar problemas que encuentre al trabajar con suscripciones, programaciones y entregas de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] .  
## <a name="log-information"></a>Información de registro
 
En la página Suscripción de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] se muestra el estado de una suscripción. Pero, si hay un problema con la suscripción, la información detallada se mostrará en los registros de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] . 
![ssrs_tutorial_datadriven_subscription_status_ReportManager](../../reporting-services/media/ssrs-tutorial-datadriven-subscription-status-reportmanager.png)

**Registros de seguimiento:** los registros de seguimiento son archivos de texto que se escriben en: `\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\LogFiles`

Este es un ejemplo de entrada de registro:

```
   subscription WindowsService_10   4c7c    05/24/2016-01:05:06  e ERROR     Failure writing file \\ServerName\SalesReports\so71949.xls : Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareProvider+NetworkErrorException: An impersonation error occurred using the security context of the current user. ---> System.ArgumentException: Value does not fall within the expected range.  05/24/2016
```
Para más información sobre los registros de seguimiento de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , vea: 
+ [Registro de seguimiento del servicio del servidor de informes](../../reporting-services/report-server/report-server-service-trace-log.md).
+ [Archivos de registro de Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md).

**Vistas del registro de ejecución:**

Los registros de ejecución son vistas en la base de datos SQL del servidor de informes. Para más información sobre [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , vea [Registro de ejecución del servidor de informes y la vista ExecutionLog3](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md).  

----------
## <a name="unable-to-send-reports-using-e-mail-with-windows-server-2003-and-pop3"></a>No se pueden enviar informes por correo electrónico con Windows 2003 Server y POP3  
Si ejecuta una aplicación de correo electrónico con Protocolo de oficina de correo 3 (POP3) en Microsoft Windows Server 2003, es posible que no pueda enviar informes utilizando el servidor POP3 local. Si configura el servidor de informes para que envíe correo electrónico con el servidor POP3 local y crea una suscripción que envía un informe, puede recibir el siguiente mensaje de error:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`Failure sending mail: <error message>`  
  
donde \<mensaje de error> se reemplaza por información de mensaje de error adicional procedente de Objetos para colaboración de datos (CDO).  
  
### <a name="to-resolve-this-problem"></a>Para resolver este problema:  
* Defina el valor del elemento `SendUsing` del archivo **Rsreportserver.config** en 1.  
* Borrar el valor de la propiedad `SMTPServer` para que esté vacía. También deberá proporcionar un valor para la propiedad `SMTPServerPickupDirectory` .   
  
Para más información sobre la utilización de un servicio SMTP local para la entrega de informes por correo electrónico, vea Configurar un servidor de informes para la entrega de correo electrónico .  
  
## <a name="failure-sending-mail-the-server-rejected-the-sender-address-the-server-response-was-454-573-client-does-not-have-permission-to-submit-mail-to-this-server"></a>Error al enviar correo: el servidor ha rechazado la dirección del remitente. La respuesta del servidor fue: 454 5.7.3 El cliente no tiene permiso para enviar correo a este servidor  
Este error se produce cuando la configuración de las directivas de seguridad en el servidor SMTP solamente permite que usuarios autenticados envíen correo para su entrega posterior. Si el servidor SMTP no admite envíos de correo procedentes de usuarios anónimos, consulte al administrador del sistema cómo obtener permiso para utilizar el servidor.  
> Este error se produce al especificar un nombre de servidor Exchange como SMTPServer. Para utilizar un servidor Exchange para la entrega por correo electrónico es preciso especificar el nombre de la puerta de enlace SMTP configurada en el servidor Exchange. Consulte al administrador de Exchange para obtener esta información.  
  
## <a name="subscriptions-are-not-processing"></a>No se procesan las suscripciones  
Las suscripciones pueden no llevarse a cabo en estas circunstancias.   
* La programación utilizada para desencadenar el informe ha expirado. En el caso de suscripciones que se desencadenen con una actualización de instantánea de informe, podría haber expirado la programación utilizada para actualizar la instantánea.  
  
* No se está ejecutando el servidor de informes, el Agente SQL Server o la aplicación del servidor de correo electrónico.  
* No se puede entregar el mensaje (por ejemplo, es demasiado grande). Para determinar si se produce un error de entrega porque el informe es demasiado grande, guárdelo en un archivo y envíelo por correo electrónico. Asegúrese de elegir el mismo formato de representación especificado en la suscripción. Si aparece un error de entrega, utilice la extensión de entrega a recursos compartidos de archivos en lugar de la extensión de entrega por correo electrónico del servidor de informes.  
* El equipo utilizado para la entrega de recurso compartido de archivos no está en funcionamiento o el recurso compartido de archivos está configurado para acceso de solo lectura.  
* La extensión de entrega especificada en la suscripción se ha desinstalado o deshabilitado.  
* La configuración de las credenciales ha cambiado de almacenadas a integradas o solicitadas.  
* El tipo de datos o el nombre del parámetro ha cambiado en la definición del informe y se ha vuelto a publicar el informe. Si una suscripción incluye un parámetro que ya no es válido, la suscripción queda inactiva.  
  
Para más información, vea [Solucionar problemas y errores con Reporting Services](https://social.technet.microsoft.com/wiki/contents/articles/1633.ssrs-troubleshoot-issues-and-errors-with-reporting-services.aspx)en el wiki de TechNet.  
  
  
    
  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

