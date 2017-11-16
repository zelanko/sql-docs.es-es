---
title: "Configuración de la opción de configuración del servidor Archivo de datos remotos | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b5817b5a-f39a-4faf-b11e-a47b54fd9f32
caps.latest.revision: "8"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3f86893797913daca2eb43826ce7597b7eee298d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="configure-the-remote-data-archive-server-configuration-option"></a>Configuración de la opción de configuración del servidor Archivo de datos remotos
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Utilice la opción **remote data archive** para especificar si las bases de datos y tablas del servidor pueden habilitarse para Stretch. Para obtener más información, vea [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md).  
  
 La opción **remote data archive** puede tener los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|0|Las bases de datos y las tablas del servidor no pueden habilitarse para Stretch.|  
|1|Las bases de datos y las tablas del servidor pueden habilitarse para Stretch.|  
  
 Para ejecutar **sp_configure** a fin de establecer el valor de la opción **remote data archive** , se necesitan permisos de administrador del sistema o administrador del servidor.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente primero se muestra la configuración actual de la opción **remote data archive** . En el mismo ejemplo luego se habilita la opción **remote data archive** estableciendo su valor en 1.  
  
```  
EXEC sp_configure 'remote data archive';  
GO  
EXEC sp_configure 'remote data archive' , '1';  
GO  
RECONFIGURE;  
GO  
```  
  
 Para deshabilitar la opción, establezca el valor en 0.  
  
## <a name="see-also"></a>Vea también  
 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
