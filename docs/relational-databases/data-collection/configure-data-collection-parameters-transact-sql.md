---
title: Configurar parámetros para la recopilación de datos (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- data collection [SQL Server]
ms.assetid: 850905b6-35d2-4ed1-ab51-de64daa832b2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 31d9f661908adc148fea48b020fa8b8b215c4755
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909697"
---
# <a name="configure-data-collection-parameters-transact-sql"></a>Configurar parámetros para la recopilación de datos (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Antes de crear un conjunto de recopilación personalizado, primero debe configurar los parámetros de recopilación de datos. Puede hacerlo mediante los procedimientos almacenados que se proporcionan con el recopilador de datos. Para realizar esta tarea debe usar el Editor de consultas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y llevar a cabo el siguiente procedimiento.  
  
> [!NOTE]  
>  Solo se configuran una vez los parámetros de recopilación de datos. Tras la configuración, esos parámetros se usan para cualquier conjunto de recopilación adicional que cree.  
  
### <a name="configure-data-collection-parameters"></a>Configurar parámetros para la recopilación de datos  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a la base de datos donde desea crear un conjunto de recopilación personalizado.  
  
2.  En el Editor de consultas, emita las instrucciones siguientes.  

    ```sql  
    USE msdb;  
    EXEC sp_syscollector_set_warehouse_instance_name N'INSTANCE_NAME';-- where instance name is the name of the SQL Server instance  
    EXEC sp_syscollector_set_warehouse_database_name N'MDW';  
    EXEC sp_syscollector_set_cache_directory N'D:\tempdata';  
    ```  
  
## <a name="see-also"></a>Consulte también  
 [Recopilación de datos](../../relational-databases/data-collection/data-collection.md)   
 [Procedimientos almacenados del recopilador de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)  
  
  
