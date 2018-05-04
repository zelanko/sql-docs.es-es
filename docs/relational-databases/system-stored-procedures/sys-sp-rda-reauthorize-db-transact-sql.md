---
title: Sys.sp_rda_reauthorize_db (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_rda_reauthorize_db
- sp_rda_reauthorize_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reauthorize_db stored procedure
ms.assetid: f6f3e4b2-8c72-4d23-a5de-fe671ca5c5cd
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e8e68eef4e198ab55a6fa465abd07afa16918a21
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="syssprdareauthorizedb-transact-sql"></a>Sys.sp_rda_reauthorize_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Restaura la conexión autenticada entre una base de datos local habilitada para Stretch y la base de datos remota.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_rda_reauthorize_db @credential = @credential, @with_copy = @with_copy [ , @azure_servername = @azure_servername, @azure_databasename = @azure_databasename ]  
```  
  
## <a name="arguments"></a>Argumentos  
 @credential = *@credential*  
 Es la credencial de ámbito de la base de datos asociada con la base de datos habilitada para Stretch local.  
  
 @with_copy = *@with_copy*  
 Especifica si se debe realizar una copia de los datos remotos y conectarse a la copia (recomendada). *@with_copy* es de tipo bit.  
  
 @azure_servername = *@azure_servername*  
 Especifica el nombre del servidor de Azure que contiene los datos remotos. *@azure_servername* es de tipo sysname.  
  
 @azure_databasename = *@azure_databasename*  
 Especifica el nombre de la base de datos de Azure que contiene los datos remotos. *@azure_databasename* es de tipo sysname.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o >0 (error)  
  
## <a name="permissions"></a>Permissions  
 Se requieren permisos db_owner.  
  
## <a name="remarks"></a>Comentarios  
 Al ejecutar [sys.sp_rda_reauthorize_db (Transact-SQL)](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) para volver a conectarse a la base de datos de Azure remota, esta operación restablece automáticamente el modo de consulta a LOCAL_AND_REMOTE, que es el comportamiento predeterminado para la base de datos de Stretch. Es decir, las consultas devuelven resultados de datos locales y remotos.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se restaura la conexión autenticada entre una base de datos local habilitada para Stretch y la base de datos remota. Realiza una copia de los datos remotos (recomendados) y se conecta a la nueva copia.  
  
```sql  
DECLARE @credentialName nvarchar(128);   
SET @credentialName = N'<existing_database_scoped_credential_name>';   
EXEC sp_rda_reauthorize_db @credential = @credentialName, @with_copy = 1;  
  
```  
  
## <a name="see-also"></a>Vea también  
 [sys.sp_rda_deauthorize_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
