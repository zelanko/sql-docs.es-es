---
title: User Settable (objeto de SQL Server) | Microsoft Docs
description: Obtenga información sobre el objeto User Settable, que crea instancias de contadores personalizadas en SQL Server para supervisar los aspectos del servidor que los contadores existentes no supervisan.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- User Settable object
- SQLServer:User Settable
ms.assetid: 633de3ef-533c-4f0c-9c7b-c105129d8e94
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: f61f4013c02148485994ebcb5b579c0d0ef78b2b
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458637"
---
# <a name="sql-server-user-settable-object"></a>User Settable (objeto de SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  El objeto **User Settable** de Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite crear instancias de contadores personalizadas. Utilice las instancias de contadores personalizadas para supervisar aspectos del servidor que los contadores existentes no supervisan, como los componentes únicos de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (por ejemplo, para determinar el número de pedidos de clientes registrados o el inventario de productos).  
  
 El objeto **User Settable** contiene 10 instancias del contador de consultas: **Contador de usuario 1** hasta **Contador de usuario 10**. Estos contadores tienen asignados los procedimientos almacenados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que van del **sp_user_counter1** al **sp_user_counter10**. A medida que las aplicaciones del usuario ejecutan estos procedimientos almacenados, los valores que establecen estos procedimientos almacenados se muestran en el Monitor de sistema. Un contador puede supervisar cualquier valor entero, por ejemplo, un procedimiento almacenado que cuente el número de pedidos de un producto específico que se han realizado en un día.  
  
> [!NOTE]  
>  El Monitor del sistema no realiza automáticamente el sondeo de los procedimientos almacenados de contadores del usuario. Es necesario ejecutarlos explícitamente en una aplicación de usuario para actualizar los valores de estos contadores. Utilice un desencadenador para actualizar automáticamente el valor del contador. Por ejemplo, para crear un contador que supervise el número de filas de una tabla, cree un desencadenador INSERT y DELETE en la tabla que ejecuta la siguiente instrucción: `SELECT COUNT(*) FROM table`. Siempre que se active el desencadenador debido a que se esté realizando una operación INSERT o DELETE en la tabla, el contador del Monitor de sistema se actualizará automáticamente.  
  
 En esta tabla se describe el objeto **User Settable** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Contadores de Establecidas por el usuario de SQL Server|Descripción|  
|---------------------------------------|-----------------|  
|**Consultar**|El objeto **User Settable** contiene el contador de consultas. El usuario configura los **contadores del usuario** del objeto Query.|  
  
 En esta tabla se describen las **instancias** del contador **Consulta** .  
  
|Instancias del contador de consultas|Descripción|  
|-----------------------------|-----------------|  
|**User counter 1**|Definido mediante **sp_user_counter1**.|  
|**User counter 2**|Definido mediante **sp_user_counter2**.|  
|**User counter 3**|Definido mediante **sp_user_counter3**.|  
|...||  
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
  
## <a name="see-also"></a>Consulte también  
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
