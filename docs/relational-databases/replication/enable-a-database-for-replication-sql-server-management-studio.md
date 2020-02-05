---
title: Habilitación de una base de datos para replicación (SSMS)
description: Obtenga información sobre cómo habilitar una base de datos para la replicación mediante SQL Server Management Studio (SSMS) o Transact-SQL (T-SQL).
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server replication]
ms.assetid: 8092faa3-9cff-4f81-926c-6a0070d1ce2c
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 03c532b6dcb0ad55a39afdae71f6879d7bc327cc
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "76288382"
---
# <a name="enable-a-database-for-replication-sql-server-management-studio"></a>Habilitar una base de datos para replicación (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  
Una base de datos se habilita de forma implícita para replicación cuando un miembro del rol fijo de servidor **sysadmin** crea una publicación con el Asistente para nueva publicación. Un miembro del rol fijo de servidor **sysadmin** también puede habilitar una base de datos para replicación de forma explícita, de manera que un miembro del rol fijo de base de datos **db_owner** pueda crear una o varias publicaciones en esa base de datos. Para habilitar una base de datos de forma explícita, utilice la página **Bases de datos de publicación** del cuadro de diálogo **Propiedades del publicador: \<Publicador>** . Para obtener más información sobre el acceso a este cuadro de diálogo, vea [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
## <a name="using-sql-server-management-studio-ssms"></a>Usar SQL Server Management Studio (SSMS)
  
1.  En la página **Bases de datos de publicación** del cuadro de diálogo **Propiedades del publicador: \<Publicador>** , active las casillas **Transaccional** y/o **Mezclar** para cada una de las bases de datos que desee replicar. Active la casilla **Transaccional** para habilitar la base de datos para replicación de instantáneas.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  
## <a name="using-transact-sql-t-sql"></a>Uso de Transact-SQL (T-SQL)
Puede habilitar una base de datos para replicarla con el siguiente código Transact-SQL: 

```sql
USE master
EXEC sp_replicationdboption @dbname = 'AdventureWorks2017',
@optname = 'publish',
@value = 'true'
GO
```

Para deshabilitar la publicación, establezca @value = 'false'. 
