---
title: Trabajar con administradores de conexiones mediante programación | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- connection managers [Integration Services], programming
ms.assetid: 2686fe84-1ecc-48b8-9160-e7122274bd84
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 973cb7dcfe7eb95e003428adf0c8a0beb7e68e87
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62877719"
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
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|Administrador de conexiones de [!INCLUDE[vstecado](../includes/vstecado-md.md)]|`System.Data.SqlClient.SqlConnection`||  
|FILE|administrador de conexiones de archivos|`System.String`|Ruta de acceso al archivo.|  
|FLATFILE|Administrador de conexiones de archivos planos|`System.String`|Ruta de acceso al archivo.|  
|MSMQ|MSMQ, administrador de conexiones|`System.Messaging.MessageQueue`||  
|MULTIFILE|administrador de conexiones de varios archivos|`System.String`|Ruta de acceso a uno de los archivos.|  
|MULTIFLATFILE|administrador de conexiones de varios archivos planos|`System.String`|Ruta de acceso a uno de los archivos.|  
|SMOServer|SMO, administrador de conexiones|`Microsoft.SqlServer.Management.Smo.Server`||  
|SMTP|Administrador de conexiones SMTP|`System.String`|Por ejemplo: `SmtpServer=<server name>;UseWindowsAuthentication=True;EnableSsl=False;`|  
|WMI|Administrador de conexiones WMI|`System.Management.ManagementScope`||  
|SQLMOBILE|Administrador de conexiones de SQL Server Compact|`System.Data.SqlServerCe.SqlCeConnection`||  
  
![Integration Services icono (pequeño)](media/dts-16.gif "Icono de Integration Services (pequeño)")  **Manténgase al día con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Consulte también  
 [Conexión a orígenes de datos en la tarea script](extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)   
 [Conectarse a orígenes de datos en el componente de script](extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)   
 [Conectarse a orígenes de datos de una tarea personalizada](extending-packages-custom-objects/task/connecting-to-data-sources-in-a-custom-task.md)  
  
  
