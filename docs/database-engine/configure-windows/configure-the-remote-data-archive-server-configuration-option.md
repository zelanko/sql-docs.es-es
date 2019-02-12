---
title: Configuración de la opción de configuración del servidor Archivo de datos remotos | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 0aa939d36a97f6d4b7f0587bd06470189b91ff3b
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56017997"
---
# <a name="configure-the-remote-data-archive-server-configuration-option"></a>Configuración de la opción de configuración del servidor Archivo de datos remotos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="see-also"></a>Consulte también  
 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
