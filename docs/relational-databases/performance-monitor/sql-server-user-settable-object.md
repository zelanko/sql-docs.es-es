---
title: User Settable (objeto de SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- User Settable object
- SQLServer:User Settable
ms.assetid: 633de3ef-533c-4f0c-9c7b-c105129d8e94
caps.latest.revision: "22"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4d60d2059230ed74f72ef4e5ad7f32a3f91aa40b
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-user-settable-object"></a>User Settable (objeto de SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] El objeto **User Settable** de Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite crear instancias de contadores personalizadas. Utilice las instancias de contadores personalizadas para supervisar aspectos del servidor que los contadores existentes no supervisan, como los componentes únicos de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (por ejemplo, para determinar el número de pedidos de clientes registrados o el inventario de productos).  
  
 El objeto **User Settable** contiene diez instancias del contador de consultas: **User counter 1** a **User counter 10**. Estos contadores tienen asignados los procedimientos almacenados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que van del **sp_user_counter1** al **sp_user_counter10**. A medida que las aplicaciones del usuario ejecutan estos procedimientos almacenados, los valores que establecen estos procedimientos almacenados se muestran en el Monitor de sistema. Un contador puede supervisar cualquier valor entero, por ejemplo, un procedimiento almacenado que cuente el número de pedidos de un producto específico que se han realizado en un día.  
  
> [!NOTE]  
>  El Monitor del sistema no realiza automáticamente el sondeo de los procedimientos almacenados de contadores del usuario. Es necesario ejecutarlos explícitamente en una aplicación de usuario para actualizar los valores de estos contadores. Utilice un desencadenador para actualizar automáticamente el valor del contador. Por ejemplo, para crear un contador que supervise el número de filas de una tabla, cree un desencadenador INSERT y DELETE en la tabla que ejecuta la siguiente instrucción: `SELECT COUNT(*) FROM table`. Siempre que se active el desencadenador debido a que se esté realizando una operación INSERT o DELETE en la tabla, el contador del Monitor de sistema se actualizará automáticamente.  
  
 En esta tabla se describe el objeto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **User Settable** .  
  
|Contadores de Establecidas por el usuario de SQL Server|Description|  
|---------------------------------------|-----------------|  
|**Consulta**|El objeto **User Settable** contiene el contador de consultas. El usuario configura los **contadores del usuario** del objeto Query.|  
  
 En esta tabla se describen las **instancias** del contador **Consulta** .  
  
|Instancias del contador de consultas|Description|  
|-----------------------------|-----------------|  
|**User counter 1**|Definido mediante **sp_user_counter1**.|  
|**User counter 2**|Definido mediante **sp_user_counter2**.|  
|**User counter 3**|Definido mediante **sp_user_counter3**.|  
|…||  
|**User counter 10**|Definido mediante **sp_user_counter10**.|  
  
 Para utilizar los procedimientos almacenados de contadores del usuario, ejecútelos desde su propia aplicación con un parámetro de número entero que represente el nuevo valor del contador. Por ejemplo, para establecer el valor 10 para **User counter 1** , ejecute esta instrucción Transact-SQL:  
  
```  
EXECUTE sp_user_counter1 10  
```  
  
 Los procedimientos almacenados de contadores de usuario se pueden llamar desde los mismos lugares que otros procedimientos almacenados, por ejemplo los propios del usuario. Por ejemplo, puede crear el siguiente procedimiento almacenado para contar el número de conexiones e intentos de conexión realizados desde que se inició una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
```  
DROP PROC My_Proc  
GO  
CREATE PROC My_Proc  
AS   
   EXECUTE sp_user_counter1 @@CONNECTIONS  
GO  
```  
  
 La función @@CONNECTIONS devuelve el número de conexiones o intentos de conexión desde el inicio de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Este valor se pasa al procedimiento almacenado **sp_user_counter1** como el parámetro.  
  
> [!IMPORTANT]  
>  Las consultas definidas en los procedimientos almacenados de contadores de usuario deben ser lo más sencillas posible. Las consultas con un gran uso de memoria que realizan un número significativo de operaciones de ordenación o de hash, o las consultas que realizan un gran número de operaciones de E/S tienen un gran costo de ejecución y pueden afectar al rendimiento.  
  
## <a name="permissions"></a>Permisos  
 **sp_user_counter** está disponible para todos los usuarios, pero puede estar restringido para cualquier contador de consultas.  
  
## <a name="see-also"></a>Ver también  
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
