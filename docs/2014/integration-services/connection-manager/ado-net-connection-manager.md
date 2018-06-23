---
title: Administrador de conexiones ADO.NET | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
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
ms.openlocfilehash: 44b07e26877a4d53d87cabb2ce48894f067a2802
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204881"
---
# <a name="adonet-connection-manager"></a>Administrador de conexiones ADO.NET
  Un administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] permite a un paquete tener acceso a orígenes de datos mediante un proveedor .NET. Este administrador de conexiones normalmente se usa para acceder a orígenes de datos como [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], así como a orígenes de datos expuestos a través de OLE DB y XML en tareas personalizadas que se escriben en código administrado con un lenguaje como C#.  
  
 Cuando se agrega un [!INCLUDE[vstecado](../../includes/vstecado-md.md)] Administrador de conexiones para un paquete, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una conexión de administrador que se resuelve como un [!INCLUDE[vstecado](../../includes/vstecado-md.md)] conexión en tiempo de ejecución, Establece propiedades del Administrador de la conexión y agrega el Administrador de conexiones el `Connections` colección en el paquete.  
  
 El `ConnectionManagerType` propiedad del Administrador de conexiones se establece en `ADO.NET`. El valor de `ConnectionManagerType` se califica para incluir el nombre del proveedor .NET que usa el Administrador de conexiones.  
  
## <a name="adonet-connection-manager-troubleshooting"></a>Solución de problemas del administrador de conexiones ADO.NET  
 Puede registrar las llamadas realizadas por el administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] a proveedores de datos externos. Puede utilizar esta capacidad de registro para solucionar problemas relacionados con las conexiones que el administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] establece con orígenes de datos externos. Para registrar las llamadas que el administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] realiza a proveedores de datos externos, habilite el registro de paquetes y seleccione el evento **Diagnostic** en el nivel de paquete. Para obtener más información, vea [Herramientas para solucionar problemas con la ejecución de paquetes](../troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
 Al ser leídos por un administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] , los datos de ciertos tipos de datos de fecha de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generarán los resultados que se muestran en la tabla siguiente.  
  
|Tipo de datos de SQL Server|Resultado|  
|--------------------------|------------|  
|`time`, `datetimeoffset`|Se produce un error en el paquete a menos que el paquete utilice comandos SQL parametrizados. Para utilizar comandos SQL parametrizados, utilice la tarea Ejecute SQL en el paquete. Para más información, vea [Tarea Ejecutar SQL](../control-flow/execute-sql-task.md) y [Parámetros y códigos de retorno en la tarea Ejecutar SQL](../parameters-and-return-codes-in-the-execute-sql-task.md).|  
|`datetime2`|El administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] trunca el valor de milisegundos.|  
  
> [!NOTE]  
>  Para más información sobre los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y cómo se asignan a los tipos de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vea [Tipos de datos &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql) y [Tipos de datos de Integration Services](../data-flow/integration-services-data-types.md).  
  
## <a name="adonet-connection-manager-configuration"></a>Configuración del administrador de conexiones ADO.NET  
 Puede configurar el administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] de las maneras siguientes:  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
-   Proporcionar una cadena de conexión específica configurada para cumplir con los requisitos del proveedor .NET seleccionado.  
  
-   Según el proveedor, incluir el nombre del origen de datos al cual conectarse.  
  
-   Proporcionar credenciales de seguridad según resulte apropiado para el proveedor seleccionado.  
  
-   Indicar si la conexión creada desde el administrador de conexiones se conserva en el tiempo de ejecución.  
  
 Muchas de las opciones de configuración del administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] dependen del proveedor .NET que usa el administrador de conexiones.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Configurar el Administrador de conexión de ADO.NET](../configure-ado-net-connection-manager.md)  
  
 Para obtener información acerca de cómo configurar un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [agregar conexiones mediante programación](../building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Vea también  
 [Servicios de integración &#40;SSIS&#41; conexiones](integration-services-ssis-connections.md)  
  
  
