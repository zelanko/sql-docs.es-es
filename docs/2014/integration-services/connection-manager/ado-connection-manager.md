---
title: Administrador de conexiones ADO | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], ADO
- connection managers [Integration Services], ADO
- ADO connection manager [Integration Services]
ms.assetid: 490418bc-5ef1-41b8-a9c8-de38aa96e0f6
caps.latest.revision: 54
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 434468c487d1dc758eeef10a04b8623c88abb529
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37243055"
---
# <a name="ado-connection-manager"></a>Administrador de conexiones ADO
  Un administrador de conexiones ADO permite a un paquete conectarse con Objetos de datos ActiveX (ADO), como un conjunto de registros. Este administrador de conexiones se usa normalmente en tareas personalizadas escritas en una versión anterior de un lenguaje, como por ejemplo, Microsoft Visual Basic 6.0 o en tareas personalizadas que forman parte de una aplicación existente que usa ADO para conectarse a un origen de datos.  
  
 Cuando se agrega un administrador de conexiones ADO a un paquete, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una conexión de administrador que se resuelve como una conexión ADO en tiempo de ejecución, Establece las propiedades del Administrador de la conexión y agrega el Administrador de conexiones a la `Connections` colección en el paquete. El `ConnectionManagerType` propiedad del Administrador de conexiones se establece en `ADO`.  
  
## <a name="troubleshooting-the-ado-connection-manager"></a>Solución de problemas del administrador de conexiones ADO  
 Al ser leídos por un administrador de conexiones ADO, los datos de determinados tipos de datos de fecha de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generarán los resultados que se muestran en la tabla siguiente.  
  
|Tipo de datos de SQL Server|Resultado|  
|--------------------------|------------|  
|`time`, `datetimeoffset`|Se produce un error en el paquete a menos que el paquete utilice comandos SQL parametrizados. Para utilizar comandos SQL parametrizados, utilice la tarea Ejecute SQL en el paquete. Para más información, vea [Tarea Ejecutar SQL](../control-flow/execute-sql-task.md) y [Parámetros y códigos de retorno en la tarea Ejecutar SQL](../parameters-and-return-codes-in-the-execute-sql-task.md).|  
|`datetime2`|El administrador de conexiones ADO trunca el valor de milisegundos.|  
  
> [!NOTE]  
>  Para obtener más información sobre los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y cómo se asignan a los tipos de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vea [Tipos de datos &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql) y [Tipos de datos de Integration Services](../data-flow/integration-services-data-types.md).  
  
## <a name="configuring-the-ado-connection-manager"></a>Configurar el Administrador de conexiones ADO  
 Puede configurar el administrador de conexiones ADO de las maneras siguientes:  
  
-   Proporcionar una cadena de conexión específica configurada para cumplir con los requisitos del proveedor seleccionado.  
  
-   Según el proveedor, incluir el nombre del origen de datos al cual conectarse.  
  
-   Proporcionar credenciales de seguridad según resulte apropiado para el proveedor seleccionado.  
  
-   Indicar si la conexión creada desde el administrador de conexiones se conserva en el tiempo de ejecución.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
-   [Configurar el administrador de conexiones OLE DB](ole-db-connection-manager.md)  
  
 Para obtener información acerca de cómo configurar un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [agregar conexiones mediante programación](../building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Vea también  
 [Servicios de integración &#40;SSIS&#41; conexiones](integration-services-ssis-connections.md)  
  
  
