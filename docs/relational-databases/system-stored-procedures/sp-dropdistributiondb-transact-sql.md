---
title: sp_dropdistributiondb (Transact-SQL) | Microsoft Docs
description: Quita una base de datos de distribución y los archivos utilizados por él si no se utilizan en otra base de datos. Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos.
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropdistributiondb_TSQL
- sp_dropdistributiondb
helpviewer_keywords:
- sp_dropdistributiondb
ms.assetid: b6dd1846-2259-4d29-93af-a70a5d25a0c5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9d9290b02c149889a488452d71ae800134d38f00
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85786969"
---
# <a name="sp_dropdistributiondb-transact-sql"></a>sp_dropdistributiondb (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Quita una base de datos de distribución. Quita los archivos físicos que utiliza la base de datos si no son usados por ninguna otra base de datos. Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_dropdistributiondb [ @database= ] 'database'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @database = ] 'database'`Es la base de datos que se va a quitar. *Database* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_dropdistributiondb** se utiliza en todos los tipos de replicación.  
  
 Este procedimiento almacenado debe ejecutarse antes de quitar el distribuidor mediante la ejecución de **sp_dropdistributor**.  
  
 **sp_dropdistributiondb** también quita un trabajo agente de lectura de cola para la base de datos de distribución, si existe.  
  
 Para deshabilitar la distribución, la base de datos de distribución debe estar en línea. Si hay una instantánea de base de datos para la base de datos de distribución, debe quitarse antes de deshabilitar la distribución. Las instantáneas de base de datos son copias de solo lectura y sin conexión de bases de datos, y no están relacionadas con una instantánea de replicación. Para más información, vea [Instantáneas de base de datos &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md).  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/sp-dropdistributiondb-tr_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden ejecutar **sp_dropdistributiondb**.  
  
## <a name="see-also"></a>Consulte también  
 [Deshabilitar la publicación y distribución](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sp_adddistributiondb &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)   
 [sp_changedistributiondb &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [sp_helpdistributiondb &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
