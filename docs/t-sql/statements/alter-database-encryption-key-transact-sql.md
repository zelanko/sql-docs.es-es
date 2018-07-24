---
title: ALTER DATABASE ENCRYPTION KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/16/2018
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER_DATABASE_ENCRYPTION_KEY_TSQL
- ALTER DATABASE ENCRYPTION
- ALTER_DATABASE_ENCRYPTION_TSQL
- ALTER DATABASE ENCRYPTION KEY
dev_langs:
- TSQL
helpviewer_keywords:
- database encryption key, alter
- ALTER DATABASE ENCRYPTION KEY
ms.assetid: f88dac4b-efe0-47ed-9808-972a4381377e
caps.latest.revision: 28
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: bbaf1a75893e41b30a26ffb9173195d53c69b623
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37997467"
---
# <a name="alter-database-encryption-key-transact-sql"></a>ALTER DATABASE ENCRYPTION KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Modifica una clave de cifrado y un certificado usados para cifrar una base de datos de forma transparente. Para más información sobre el cifrado de bases de datos transparente, vea [Cifrado de datos transparente &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server  
  
ALTER DATABASE ENCRYPTION KEY  
      REGENERATE WITH ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY }  
   |  
   ENCRYPTION BY SERVER   
    {  
        CERTIFICATE Encryptor_Name |  
        ASYMMETRIC KEY Encryptor_Name  
    }  
[ ; ]  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
ALTER DATABASE ENCRYPTION KEY  
    {  
      {  
        REGENERATE WITH ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY }  
        [ ENCRYPTION BY SERVER CERTIFICATE Encryptor_Name ]  
      }  
      |  
      ENCRYPTION BY SERVER   CERTIFICATE Encryptor_Name    
    }  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 REGENERATE WITH ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY }  
 Especifica el algoritmo de cifrado utilizado para la clave de cifrado.  
  
 ENCRYPTION BY SERVER CERTIFICATE *Encryptor_Name*  
 Especifica el nombre del certificado que se usa para cifrar la clave de cifrado de base de datos.  
  
 ENCRYPTION BY SERVER ASYMMETRIC KEY Encryptor_Name  
 Especifica el nombre de la clave asimétrica que se usa para cifrar la clave de cifrado de base de datos.  
  
## <a name="remarks"></a>Notas  
 El certificado o la clave asimétrica que se usa para cifrar la clave de cifrado de base de datos se debe ubicar en la base de datos maestra del sistema.  
  
 La clave de cifrado de base de datos no tiene que regenerarse cuando se cambia el propietario de la base de datos (dbo).
  
 Cuando una clave de cifrado de base de datos se modifica dos veces, debe realizarse una copia de seguridad de registros para que la clave de cifrado de base de datos pueda volver a modificarse.  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso CONTROL en la base de datos y el permiso VIEW DEFINITION en el certificado o la clave asimétrica utilizados para cifrar la clave de cifrado de base de datos.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se modifica la clave de cifrado de base de datos para utilizar el algoritmo `AES_256`.  
  
```  
-- Uses AdventureWorks  
  
ALTER DATABASE ENCRYPTION KEY  
REGENERATE WITH ALGORITHM = AES_256;  
GO  
```  
  
## <a name="see-also"></a>Ver también  
 [Cifrado de datos transparente &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)   
 [Cifrado de SQL Server](../../relational-databases/security/encryption/sql-server-encryption.md)   
 [SQL Server y claves de cifrado de base de datos &#40;motor de base de datos&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-encryption-key-transact-sql.md)   
 [DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)   
 [sys.dm_database_encryption_keys &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md)  
  
  

