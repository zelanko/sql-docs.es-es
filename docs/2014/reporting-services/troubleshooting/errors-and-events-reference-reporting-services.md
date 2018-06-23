---
title: Referencia de errores y eventos (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- messages [Reporting Services]
- errors [Reporting Services]
- Reporting Services, errors and events
- troubleshooting [Reporting Services], errors
- events [Reporting Services]
ms.assetid: 818b4cc1-e65d-4f1a-bf7d-fe269e6dd739
caps.latest.revision: 40
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: c01067a787782649b415343a9d4c70911ebe1b57
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36114196"
---
# <a name="errors-and-events-reference-reporting-services"></a>Referencia de errores y eventos (Reporting Services)
  En este tema se proporciona información acerca de los errores y eventos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Los archivos de registro de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] también contienen información de error. Para obtener más información acerca de los tipos de archivos de registro que están disponibles y cómo ver los registros, vea [archivos de registro de servicios de informes y orígenes de](../report-server/reporting-services-log-files-and-sources.md).  
  
## <a name="cause-and-resolution-for-reporting-services-error-messages"></a>Causa y resolución de mensajes de error de Reporting Services  
 La información sobre las causas y resoluciones está disponible para los errores que se buscan con más frecuencia en los sitios web de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obtener más información, consulte [causa y resolución de Reporting Services Errors](cause-and-resolution-of-reporting-services-errors.md).  
  
## <a name="report-server-events"></a>Eventos del servidor de informes  
 En el registro de aplicación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows se incluyen los siguientes eventos del servidor de informes.  
  
|Identificador del evento|Tipo|Categoría|Source|Descripción|  
|--------------|----------|--------------|------------|-----------------|  
|106|Error|Programación|Servidor de informes|Para definir una operación programada (por ejemplo, la suscripción y entrega de un informe) es necesario que se esté ejecutando el Agente SQL Server.|  
|[107](../../relational-databases/errors-events/mssqlserver-107-database-engine-error.md)|Error|Inicio y cierre|Servidor de informes<br /><br /> Procesador de entrega y programación|*\<Origen>* no se puede conectar a la base de datos del servidor de informes. Para más información, vea [Servicio Servidor de informes de Windows &#40;MSSQLServer&#41; 107](../../relational-databases/errors-events/mssqlserver-107-database-engine-error.md).|  
|108|Error|Extensión|Servidor de informes<br /><br /> Administrador de informes|*\<Origen>* no puede cargar una extensión de entrega, de procesamiento de datos o de representación.<br /><br /> Lo más probable es que se deba a una implementación incompleta o a la eliminación de una extensión. Para obtener más información, consulte [implementar una extensión de procesamiento de datos](../extensions/data-processing/deploying-a-data-processing-extension.md) y [implementar una extensión de entrega](../extensions/delivery-extension/deploying-a-delivery-extension.md).|  
|109|Información|Administración|Servidor de informes<br /><br /> Administrador de informes|Se ha modificado un archivo de configuración. Para obtener más información, consulte [Reporting Services Configuration Files](../report-server/reporting-services-configuration-files.md).|  
|110|Advertencia|Administración|Servidor de informes<br /><br /> Administrador de informes|Se ha modificado un valor en uno de los archivos de configuración y ha dejado de ser válido. En su lugar, se utilizará un valor predeterminado. Para obtener más información, consulte [Reporting Services Configuration Files](../report-server/reporting-services-configuration-files.md).|  
|111|Error|Registro|Servidor de informes<br /><br /> Administrador de informes|*\<Origen>* no puede crear el registro de seguimiento. Para obtener más información, consulte [Report Server Service Trace Log](../report-server/report-server-service-trace-log.md).|  
|112|Advertencia|Seguridad|Servidor de informes|El servidor de informes ha detectado un posible ataque de denegación de servicio. Para obtener más información, consulte [Reporting Services Security y la protección](../security/reporting-services-security-and-protection.md).|  
|113|Error|Registro|Servidor de informes|El servidor de informes no puede crear un contador de rendimiento.|  
|114|Error|Inicio y cierre|Administrador de informes|El Administrador de informes no puede conectarse al servicio Servidor de informes.|  
|115|Advertencia|Programación|Procesador de entrega y programación|Se ha modificado o eliminado una tarea programada de la cola del Agente SQL Server.|  
|116|Error|Interno|Servidor de informes<br /><br /> Administrador de informes<br /><br /> Procesador de entrega y programación|Error interno.|  
|117|Error|Inicio y cierre|Servidor de informes|La base de datos del servidor de informes tiene una versión no válida.|  
|118|Advertencia|Registro|Servidor de informes<br /><br /> Administrador de informes|El registro de seguimiento no se encuentra en la ubicación esperada del directorio; se creará un nuevo registro de seguimiento en el directorio predeterminado. Para obtener más información, consulte [Report Server Service Trace Log](../report-server/report-server-service-trace-log.md).|  
|119|Error|Activación|Servidor de informes<br /><br /> Procesador de entrega y programación|*\<Origen>* no tiene acceso al contenido de la base de datos del servidor de informes.|  
|120|Error|Activación|Servidor de informes|No se puede descifrar la clave simétrica. Probablemente se haya producido un cambio en la cuenta con la que se ejecuta el servicio. Para más información, vea [Configurar y administrar claves de cifrado &#40;Administrador de configuración de SSRS&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
|121|Error|Inicio y cierre|Servidor de informes|No se pudo iniciar el servicio de llamada a procedimiento remoto (RPC).|  
|122|Advertencia|Entrega|Procesador de entrega y programación|El Procesador de entrega y programación no se puede conectar al servidor SMTP que se utiliza para la entrega por correo electrónico. Para obtener más información acerca de las conexiones de servidor SMTP, vea [configurar un servidor de informes para la entrega de correo electrónico &#40;Administrador de configuración de SSRS&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md).|  
|123|Advertencia|Registro|Servidor de informes<br /><br /> Administrador de informes|El servidor de informes no pudo escribir en el registro de seguimiento. Para obtener más información acerca de los registros de seguimiento, vea [Report Server Service Trace Log](../report-server/report-server-service-trace-log.md).|  
|124|Información|Activación|Servidor de informes|Se ha inicializado el servicio Servidor de informes. Para más información, vea [Inicializar un servidor de informes &#40;Administrador de configuración de SSRS&#41;](../install-windows/ssrs-encryption-keys-initialize-a-report-server.md).|  
|125|Información|Activación|Servidor de informes|Se extrajo correctamente la clave utilizada para cifrar datos. Para más información sobre las claves, vea [Configurar y administrar claves de cifrado &#40;Administrador de configuración de SSRS&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
|126|Información|Activación|Servidor de informes|Se aplicó correctamente la clave utilizada para cifrar datos. Para más información sobre las claves, vea [Configurar y administrar claves de cifrado &#40;Administrador de configuración de SSRS&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
|127|Información|Activación|Servidor de informes|Se quitó correctamente el contenido cifrado de la base de datos del servidor de informes. Para más información sobre cómo eliminar datos cifrados no recuperables, vea [Configurar y administrar claves de cifrado &#40;Administrador de configuración de SSRS&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
|128|Error|Activación|Servidor de informes|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de diferentes ediciones no se pueden usar en conjunto.|  
|129|Error|Administración|Servidor de informes<br /><br /> Procesador de entrega y programación|Un valor de archivo de configuración cifrado no se puede descifrar.|  
|130|Error|Administración|Servidor de informes<br /><br /> Procesador de entrega y programación|*\<Origen>* no encuentra el archivo de configuración. El servidor de informes requiere archivos de configuración.|  
|131|Error|Seguridad|Servidor de informes<br /><br /> Procesador de entrega y programación|No se pudo descifrar un valor de datos de usuario cifrado.|  
|132|Error|Seguridad|Servidor de informes|Error al cifrar los datos de usuario. No se puede guardar el valor.|  
|133|Error|Administración|Servidor de informes<br /><br /> Administrador de informes<br /><br /> Procesador de entrega y programación|Error al cargar un archivo de configuración. Este error puede producirse si el código XML no es válido.|  
|134|Error|Administración|Servidor de informes|El servidor de informes no pudo cifrar valores para un valor de un archivo de configuración.|  
  
## <a name="see-also"></a>Vea también  
 [Supervisar suscripciones de Reporting Services](../subscriptions/monitor-reporting-services-subscriptions.md)   
 [Archivos de registro y orígenes de Reporting Services](../report-server/reporting-services-log-files-and-sources.md)  
  
  