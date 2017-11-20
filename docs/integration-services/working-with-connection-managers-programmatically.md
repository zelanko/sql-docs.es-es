---
title: "Trabajar con administradores de conexión mediante programación | Documentos de Microsoft"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- connection managers [Integration Services], programming
ms.assetid: 2686fe84-1ecc-48b8-9160-e7122274bd84
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9093b9eadce231aea248cd04c2b57dc5dd5e1a76
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="working-with-connection-managers-programmatically"></a>Trabajar con administradores de conexiones mediante programación
  En [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], el método AcquireConnection de la clase del Administrador de conexión asociado es el método que llama con mayor frecuencia cuando se trabaja con administradores de conexión en código administrado. Cuando se escribe código administrado, tendrá que llamar el método AcquireConnection para usar la funcionalidad de una conexión de administrador. Debe llamar a este método independientemente de si escribe el código administrado en una tarea Script, un componente de script, un objeto personalizado o una aplicación personalizada.  
  
 Para llamar correctamente a la llamada del método AcquireConnection, tiene que conocer las respuestas a las siguientes preguntas:  
  
-   **¿Los administradores de conexión devuelven un objeto administrado desde el método AcquireConnection?**  
  
     Muchos administradores de conexión devuelven objetos COM no administrados (System.__ComObject) y estos objetos no se puede usar fácilmente desde el código administrado. La lista de estos administradores de conexiones incluye el administrador de conexiones OLE DB de uso frecuente.  
  
-   **¿Para los administradores de conexión que devuelven un objeto administrado, los objetos devuelven sus métodos AcquireConnection?**  
  
     Para convertir el valor devuelto al tipo adecuado, tendrá que saber qué tipo de objeto que devuelve el método AcquireConnection. Por ejemplo, el método AcquireConnection para la [!INCLUDE[vstecado](../includes/vstecado-md.md)] Administrador de conexiones devuelve un objeto SqlConnection abierto cuando se usa el proveedor SqlClient. Sin embargo, el método AcquireConnection para el Administrador de conexiones de archivos solamente devuelve una cadena.  
  
 En este tema se responden estas preguntas sobre los administradores de conexiones incluidos con [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
## <a name="connection-managers-that-do-not-return-a-managed-object"></a>Administradores de conexiones que no devuelven un objeto administrado  
 En la tabla siguiente se enumera los administradores de conexión que devuelven un objeto COM nativo (System.__ComObject) desde el método AcquireConnection. Estos objetos no administrados no resultan fáciles de usar desde código administrado.  
  
|Tipo de administrador de conexiones|Nombre del Administrador de conexiones|  
|-----------------------------|-----------------------------|  
|ADO|Administrador de conexiones ADO|  
|MSOLAP90|Administrador de conexiones de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|  
|EXCEL|Administrador de conexiones con Excel|  
|FTP|FTP, administrador de conexiones|  
|HTTP|HTTP, administrador de conexiones|  
|ODBC|ODBC, administrador de conexiones|  
|OLEDB|OLE DB, administrador de conexiones|  
  
 Por lo general, puede usar un [!INCLUDE[vstecado](../includes/vstecado-md.md)] connection manager desde el código administrado para conectarse a un origen de datos ADO, Excel, ODBC u OLE DB.  
  
## <a name="return-values-from-the-acquireconnection-method"></a>Valores devueltos del método AcquireConnection  
 En la tabla siguiente se enumera los administradores de conexión que devuelven un objeto administrado desde el método AcquireConnection. Estos objetos administrados se pueden usar con facilidad desde código administrado.  
  
|Tipo de administrador de conexiones|Nombre del Administrador de conexiones|Tipo de valor devuelto|Información adicional|  
|-----------------------------|-----------------------------|--------------------------|----------------------------|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|Administrador de conexiones de [!INCLUDE[vstecado](../includes/vstecado-md.md)]|**System.Data.SqlClient.SqlConnection**||  
|FILE|administrador de conexiones de archivos|**System.String**|Ruta de acceso al archivo.|  
|FLATFILE|Administrador de conexiones de archivos planos|**System.String**|Ruta de acceso al archivo.|  
|MSMQ|MSMQ, administrador de conexiones|**System.Messaging.MessageQueue**||  
|MULTIFILE|administrador de conexiones de varios archivos|**System.String**|Ruta de acceso a uno de los archivos.|  
|MULTIFLATFILE|administrador de conexiones de varios archivos planos|**System.String**|Ruta de acceso a uno de los archivos.|  
|SMOServer|SMO, administrador de conexiones|**Microsoft.SqlServer.Management.Smo.Server**||  
|SMTP|Administrador de conexiones SMTP|**System.String**|Por ejemplo, `SmtpServer=<server name>;UseWindowsAuthentication=True;EnableSsl=False;`|  
|WMI|Administrador de conexiones WMI|**System.Management.ManagementScope**||  
|SQLMOBILE|Administrador de conexiones de SQL Server Compact|**System.Data.SqlServerCe.SqlCeConnection**||  
  
## <a name="see-also"></a>Vea también  
 [Conectarse a orígenes de datos de la tarea de secuencia de comandos](../integration-services/extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)   
 [Conectarse a orígenes de datos en el componente de Script](../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)   
 [Conectarse a orígenes de datos de una tarea personalizada](../integration-services/extending-packages-custom-objects/task/connecting-to-data-sources-in-a-custom-task.md)  
  
  

