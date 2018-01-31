---
title: "Trabajar con administradores de conexiones mediante programación | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- connection managers [Integration Services], programming
ms.assetid: 2686fe84-1ecc-48b8-9160-e7122274bd84
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9e71d4ed2b3ffb4caa2009770b3f753fb0d5884c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="working-with-connection-managers-programmatically"></a>Trabajar con administradores de conexiones mediante programación
  En [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], el método AcquireConnection de la clase de administradores de conexiones asociada es el método al que se llama con mayor frecuencia cuando se está trabajando con administradores de conexiones en código administrado. Al escribir código administrado, tiene que llamar al método AcquireConnection para utilizar la funcionalidad de un administrador de conexiones. Debe llamar a este método independientemente de si escribe el código administrado en una tarea Script, un componente de script, un objeto personalizado o una aplicación personalizada.  
  
 Para llamar correctamente al método AcquireConnection, tiene que conocer las respuestas a las preguntas siguientes:  
  
-   **¿Qué administradores de conexiones devuelven un objeto administrado desde el método AcquireConnection?**  
  
     Muchos administradores de conexiones devuelven objetos COM no administrados (System.__ComObject) y estos objetos no se pueden utilizar con facilidad desde el código administrado. La lista de estos administradores de conexiones incluye el administrador de conexiones OLE DB de uso frecuente.  
  
-   **En el caso de los administradores de conexiones que devuelven un objeto administrado, ¿qué objetos devuelven sus métodos AcquireConnection?**  
  
     Para convertir el valor devuelto al tipo adecuado, debe saber qué tipo de objeto devuelve el método AcquireConnection. Por ejemplo, el método AcquireConnection para el administrador de conexiones [!INCLUDE[vstecado](../includes/vstecado-md.md)] devuelve un objeto SqlConnection abierto al utilizar el proveedor SqlClient. Sin embargo, el método AcquireConnection para el administrador de conexiones de archivos solamente devuelve una cadena.  
  
 En este tema se responden estas preguntas sobre los administradores de conexiones incluidos con [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
## <a name="connection-managers-that-do-not-return-a-managed-object"></a>Administradores de conexiones que no devuelven un objeto administrado  
 En la tabla siguiente se enumeran los administradores de conexiones que devuelven un objeto COM nativo (System.__ComObject) desde el método AcquireConnection. Estos objetos no administrados no resultan fáciles de usar desde código administrado.  
  
|Tipo de administrador de conexiones|Nombre del administrador de conexiones|  
|-----------------------------|-----------------------------|  
|ADO|Administrador de conexiones ADO|  
|MSOLAP90|Administrador de conexiones de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|  
|EXCEL|Administrador de conexiones con Excel|  
|FTP|FTP, administrador de conexiones|  
|HTTP|HTTP, administrador de conexiones|  
|ODBC|ODBC, administrador de conexiones|  
|OLEDB|OLE DB, administrador de conexiones|  
  
 Normalmente, puede utilizar un administrador de conexiones [!INCLUDE[vstecado](../includes/vstecado-md.md)] desde el código administrado para conectarse a un origen de datos ADO, Excel, ODBC u OLE DB.  
  
## <a name="return-values-from-the-acquireconnection-method"></a>Valores devueltos del método AcquireConnection  
 En la tabla siguiente se enumeran los administradores de conexiones que devuelven un objeto administrado desde el método AcquireConnection. Estos objetos administrados se pueden usar con facilidad desde código administrado.  
  
|Tipo de administrador de conexiones|Nombre del administrador de conexiones|Tipo de valor devuelto|Información adicional|  
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
  
## <a name="see-also"></a>Ver también  
 [Conectarse a orígenes de datos de la tarea Script](../integration-services/extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)   
 [Conectarse a orígenes de datos del componente de script](../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)   
 [Conectarse a orígenes de datos de una tarea personalizada](../integration-services/extending-packages-custom-objects/task/connecting-to-data-sources-in-a-custom-task.md)  
  
  
