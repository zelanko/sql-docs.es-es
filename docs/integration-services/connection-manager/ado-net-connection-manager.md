---
title: Administrador de conexiones ADO.NET | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection managers [Integration Services], ADO.NET
- ADO.NET connection manager [Integration Services]
- connections [Integration Services], ADO.NET
ms.assetid: fc5daa2f-0159-4bda-9402-c87f1035a96f
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 41363d15ebb18431c658c4f990d10a1fa67260ae
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="adonet-connection-manager"></a>Administrador de conexiones ADO.NET
  Un administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] permite a un paquete tener acceso a orígenes de datos mediante un proveedor .NET. Este administrador de conexiones normalmente se usa para acceder a orígenes de datos como [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], así como a orígenes de datos expuestos a través de OLE DB y XML en tareas personalizadas que se escriben en código administrado con un lenguaje como C#.  
  
 Cuando agrega un administrador de conexiones de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] a un paquete, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un administrador de conexiones que se resuelve como una conexión de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] en tiempo de ejecución, establece las propiedades del administrador de conexiones y agrega el administrador de conexiones a la colección **Conexiones** del paquete.  
  
 La propiedad **ConnectionManagerType** del administrador de conexiones se establece en **ADO.NET**. El valor de **ConnectionManagerType** se califica para incluir el nombre del proveedor .NET que usa el administrador de conexiones.  
  
## <a name="adonet-connection-manager-troubleshooting"></a>Solución de problemas del administrador de conexiones ADO.NET  
 Puede registrar las llamadas realizadas por el administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] a proveedores de datos externos. Puede utilizar esta capacidad de registro para solucionar problemas relacionados con las conexiones que el administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] establece con orígenes de datos externos. Para registrar las llamadas que el administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] realiza a proveedores de datos externos, habilite el registro de paquetes y seleccione el evento **Diagnostic** en el nivel de paquete. Para más información, vea [Herramientas para solucionar problemas con la ejecución de paquetes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
 Al ser leídos por un administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] , los datos de ciertos tipos de datos de fecha de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generarán los resultados que se muestran en la tabla siguiente.  
  
|Tipo de datos de SQL Server|Resultado|  
|--------------------------|------------|  
|**time**, **datetimeoffset**|Se produce un error en el paquete a menos que el paquete utilice comandos SQL parametrizados. Para utilizar comandos SQL parametrizados, utilice la tarea Ejecute SQL en el paquete. Para más información, vea [Tarea Ejecutar SQL](../../integration-services/control-flow/execute-sql-task.md) y [Parámetros y códigos de retorno en la tarea Ejecutar SQL](http://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663).|  
|**datetime2**|El administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] trunca el valor de milisegundos.|  
  
> [!NOTE]  
>  Para más información sobre los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y cómo se asignan a los tipos de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vea [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md) y [Tipos de datos de Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="adonet-connection-manager-configuration"></a>Configuración del administrador de conexiones ADO.NET  
 Puede configurar el administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] de las maneras siguientes:  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
-   Proporcionar una cadena de conexión específica configurada para cumplir con los requisitos del proveedor .NET seleccionado.  
  
-   Según el proveedor, incluir el nombre del origen de datos al cual conectarse.  
  
-   Proporcionar credenciales de seguridad según resulte apropiado para el proveedor seleccionado.  
  
-   Indicar si la conexión creada desde el administrador de conexiones se conserva en el tiempo de ejecución.  
  
 Muchas de las opciones de configuración del administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] dependen del proveedor .NET que usa el administrador de conexiones.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Configurar el administrador de conexiones ADO.NET](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)  
  
 Para más información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [Agregar conexiones mediante programación](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Vea también  
 [Conexiones de Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
