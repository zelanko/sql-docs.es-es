---
title: DROP DATABASE SCOPED CREDENTIAL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/27/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP DATABASE SCOPED CREDENTIAL
- DROP_DATABASE_SCOPED_CREDENTIAL_TSQL
helpviewer_keywords:
- DROP DATABASE SCOPED CREDENTIAL statement
- credential [SQL Server], DROP DATABASE SCOPED CREDENTIAL statement
ms.assetid: 319d59f4-fa82-47ca-869b-3a9cd52900b0
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: bab6abe83478c0f391d37a816c52f042f72b18b2
ms.sourcegitcommit: bc10ec0be5ddfc5f0bc220a9ac36c77dd6b80f1d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2020
ms.locfileid: "87544398"
---
# <a name="drop-database-scoped-credential-transact-sql"></a>DROP DATABASE SCOPED CREDENTIAL (Transact-SQL)
[!INCLUDE [asdb-asdbmi-asa](../../includes/applies-to-version/asdb-asdbmi-asa.md)]

  Quita del servidor una credencial de ámbito de base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP DATABASE SCOPED CREDENTIAL credential_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *credential_name*  
 Se trata del nombre de la credencial de ámbito de base de datos que se va a quitar del servidor.  
  
## <a name="remarks"></a>Observaciones  
 Para quitar el secreto asociado a la credencial de ámbito de base de datos sin quitar la credencial en cuestión, use [ALTER CREDENTIAL](../../t-sql/statements/alter-credential-transact-sql.md).  
  
 Encontrará información sobre las credenciales de ámbito de base de datos en la vista de catálogo [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md).  
  
## <a name="permissions"></a>Permisos  
 Necesita el permiso `ALTER` en la credencial.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se quita una credencial de ámbito de base de datos denominada `SalesAccess`.  
  
```sql  
DROP DATABASE SCOPED CREDENTIAL SalesAccess;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Credenciales &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [ALTER DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
