---
title: Sys. sp_rda_reauthorize_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sp_rda_reauthorize_db
- sp_rda_reauthorize_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reauthorize_db stored procedure
ms.assetid: f6f3e4b2-8c72-4d23-a5de-fe671ca5c5cd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 68267f07c125e05f235c1a0bcb4c7f855274bc86
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82814765"
---
# <a name="syssp_rda_reauthorize_db-transact-sql"></a>sys.sp_rda_reauthorize_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Restaura la conexión autenticada entre una base de datos local habilitada para Stretch y la base de datos remota.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_rda_reauthorize_db @credential = @credential, @with_copy = @with_copy [ , @azure_servername = @azure_servername, @azure_databasename = @azure_databasename ]  
```  
  
## <a name="arguments"></a>Argumentos  
 @credential= * \@ credencial*  
 Es la credencial con ámbito de base de datos asociada con la base de datos habilitada para Stretch local.  
  
 @with_copy= * \@ with_copy*  
 Especifica si se debe hacer una copia de los datos remotos y conectarse a la copia (recomendado). * \@ with_copy* es bit.  
  
 @azure_servername= * \@ azure_servername*  
 Especifica el nombre del servidor de Azure que contiene los datos remotos. * \@ azure_servername* es de tipo sysname.  
  
 @azure_databasename= * \@ azure_databasename*  
 Especifica el nombre de la base de datos de Azure que contiene los datos remotos. * \@ azure_databasename* es de tipo sysname.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o >0 (error)  
  
## <a name="permissions"></a>Permisos  
 Requiere permisos de db_owner.  
  
## <a name="remarks"></a>Comentarios  
 Al ejecutar [Sys. sp_rda_reauthorize_db (Transact-SQL)](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) para volver a conectar con la base de datos remota de Azure, esta operación restablece automáticamente el modo de consulta a LOCAL_AND_REMOTE, que es el comportamiento predeterminado para Stretch Database. Es decir, las consultas devuelven los resultados de los datos locales y remotos.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se restaura la conexión autenticada entre una base de datos local habilitada para Stretch y la base de datos remota. Realiza una copia de los datos remotos (recomendado) y se conecta a la nueva copia.  
  
```sql  
DECLARE @credentialName nvarchar(128);   
SET @credentialName = N'<existing_database_scoped_credential_name>';   
EXEC sp_rda_reauthorize_db @credential = @credentialName, @with_copy = 1;  
  
```  
  
## <a name="see-also"></a>Consulte también  
 [Sys. sp_rda_deauthorize_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
