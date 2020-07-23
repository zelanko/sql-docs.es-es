---
title: Administrador de conexiones con SQL Server Compact Edition | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sqlmobileconnection.connection.f1
- sql13.dts.designer.sqlmobileconnection.all.f1
helpviewer_keywords:
- SQL Server Compact, connection manager
- connections [Integration Services], SQL Server Compact
- connection managers [Integration Services], SQL Server Compact
ms.assetid: ba627d4d-41f4-49fc-a921-f534cde67770
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 777c360fd17082c06ff9aa4b0356ff3a95cbd332
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917211"
---
# <a name="sql-server-compact-edition-connection-manager"></a>Administrador de conexiones con SQL Server Compact Edition

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Un administrador de conexiones con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact habilita un paquete para establecer conexión con una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact. El destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye usa este administrador de conexiones para cargar datos en una tabla de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
> [!NOTE]  
>  En un equipo de 64 bits, necesita ejecutar paquetes que se conecten a los orígenes de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact en modo de 32 bits. El proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact que usa [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para establecer conexión con orígenes de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact solo está disponible en una versión de 32 bits.  
  
## <a name="configuration-the-sql-server-compact-edition-connection-manager"></a>Configuración del administrador de conexiones con SQL Server Compact Edition  
 Al agregar un administrador de conexiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact a un paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un administrador de conexiones que se resolverá como una conexión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact en tiempo de ejecución, establece las propiedades del administrador de conexiones y agrega el administrador de conexiones a la colección **Connections** del paquete.  
  
 La propiedad **ConnectionManagerType** del administrador de conexiones se establece en **SQLMOBILE**.  
  
 Puede configurar el administrador de conexiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact de las maneras siguientes:  
  
-   Proporcionar una cadena de conexión que especifica la ubicación de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
-   Proporcionar una contraseña para una base de datos protegida por contraseña.  
  
-   Especificar el servidor en el que se va a almacenar la base de datos.  
  
-   Indicar si la conexión creada desde el administrador de conexiones se conserva en el tiempo de ejecución.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [Agregar conexiones mediante programación](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="sql-server-compact-edition-connection-manager-editor-connection-page"></a>Editor del administrador de conexiones con SQL Server Compact Edition (página Conexión)
  Use el cuadro de diálogo **Administrador de conexiones con SQL Server Compact Edition** para especificar las propiedades de conexiones a una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
 Para obtener más información acerca del administrador de conexiones con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact Edition, vea [Administrador de conexiones con SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md).  
  
### <a name="options"></a>Opciones  
 **Especifique el nombre y la ruta del archivo de base de datos**  
 Escriba la ruta de acceso y el nombre de archivo de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
 **Browse**  
 Busque el archivo de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact deseado mediante el cuadro de diálogo **Select SQL Server Compact Edition database** (Seleccionar la base de datos de SQL Server Compact Edition).  
  
 **Escriba la contraseña de la base de datos**  
 Escriba la contraseña de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
## <a name="sql-server-compact-edition-connection-manager-editor-all-page"></a>Editor del administrador de conexiones con SQL Server Compact Edition (página Todo)
  Use el cuadro de diálogo **Administrador de conexiones con SQL Server Compact Edition** para especificar las propiedades de conexiones a una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
 Para obtener más información acerca del administrador de conexiones con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact Edition, vea [Administrador de conexiones con SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md).  
  
### <a name="options"></a>Opciones  
 **AutoShrink Threshold**  
 Especifique la cantidad de espacio disponible, como porcentaje, permitido en la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact antes de que se ejecute el proceso de reducción automática.  
  
 **Extensión de bloqueo predeterminada**  
 Especifique el número de bloqueos de base de datos que adquiere la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact antes de intentar concentrar los bloqueos.  
  
 **Default Lock Timeout**  
 Especifique el intervalo predeterminado, en milisegundos, que una transacción esperará un bloqueo.  
  
 **Flush Interval**  
 Especifique el intervalo, en segundos, transcurrido entre que las transacciones confirmadas vacían datos en el disco.  
  
 **Identificador de configuración regional**  
 Especifique el identificador de configuración regional (LCID) de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
 **Max Buffer Size**  
 Especifique la cantidad máxima de memoria, en kilobytes, que usará [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact antes del vaciado de datos en el disco.  
  
 **Max Database Size**  
 Especifique el tamaño máximo, en megabytes, de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
 **Modo**  
 Especifique el modo de archivo en el que se abrirá la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact. El valor predeterminado para esta propiedad es **Lectura y escritura**.  
  
 La opción Modo tiene cuatro valores, tal como se describe en la siguiente tabla.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Solo lectura**|Especifica acceso de solo lectura a la base de datos.|  
|**Lectura y escritura**|Especifica permiso de lectura/escritura a la base de datos.|  
|**Exclusivo**|Especifica acceso exclusivo a la base de datos.|  
|**Shared Read**|Especifica que otros usuarios pueden leer de la base de datos al mismo tiempo.|  
  
 **Persist Security Info**  
 Especifique si la información de seguridad será devuelta como parte de la cadena de conexión. El valor predeterminado de esta opción es **False**.  
  
 **Temp File Directory**  
 Especifique la ubicación del archivo de base de datos temporal de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
 **Data Source** (Origen de datos)  
 Especifique el nombre de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
 **Contraseña**  
 Escriba la contraseña de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
