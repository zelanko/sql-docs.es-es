---
title: Configuración de la opción de configuración del servidor Archivo de datos remotos | Microsoft Docs
description: Obtenga información sobre cómo usar la opción "remote data archive" en SQL Server para especificar si las bases de datos y las tablas en el servidor pueden habilitarse para Stretch.
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: b5817b5a-f39a-4faf-b11e-a47b54fd9f32
author: rothja
ms.author: jroth
ms.openlocfilehash: fc53b5392d6bd493b634e9e2c8a4a92613eb8c32
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85785744"
---
# <a name="configure-the-remote-data-archive-server-configuration-option"></a>Configuración de la opción de configuración del servidor Archivo de datos remotos
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Utilice la opción **remote data archive** para especificar si las bases de datos y tablas del servidor pueden habilitarse para Stretch. Para obtener más información, vea [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md).  
  
 La opción **remote data archive** puede tener los siguientes valores.  
  
|Value|Descripción|  
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
  
## <a name="see-also"></a>Consulte también  
 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
