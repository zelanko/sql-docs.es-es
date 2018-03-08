---
title: FIRMA de DROP (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP SIGNATURE
- DROP_SIGNATURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting signatures
- dropping signatures
- DROP SIGNATURE statement
- removing signatures
- signatures [SQL Server]
- digital signatures [SQL Server]
ms.assetid: 8a1fd8c5-0e75-4b2f-9d3c-c296bed56cc7
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e9c58cc536c6ffa929dce2466f8a7c4c27528ba4
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="drop-signature-transact-sql"></a>DROP SIGNATURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Quita una firma digital de un procedimiento almacenado, una función, un desencadenador o un ensamblado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP [ COUNTER ] SIGNATURE FROM module_name   
    BY <crypto_list> [ ,...n ]  
  
<crypto_list> ::=  
    CERTIFICATE cert_name  
    | ASYMMETRIC KEY Asym_key_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *Nombre_Del_Módulo*  
 Es el nombre de un procedimiento almacenado, una función, un ensamblado o un desencadenador.  
  
 CERTIFICADO *cert_name*  
 Es el nombre de un certificado con el que está firmado el procedimiento almacenado, la función, el ensamblado o el desencadenador.  
  
 CLAVE ASIMÉTRICA *Asym_key_name*  
 Es el nombre de una clave asimétrica con la que está firmado el procedimiento almacenado, la función, el ensamblado o el desencadenador.  
  
## <a name="remarks"></a>Comentarios  
 Para obtener más información acerca de las firmas, vea la vista de catálogo sys.crypt_properties.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER para el objeto y el permiso CONTROL para el certificado o la clave asimétrica. Si una clave privada asociada está protegida por una contraseña, el usuario también debe tener la contraseña.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se quita la firma del certificado `HumanResourcesDP` desde el procedimiento almacenado `HumanResources.uspUpdateEmployeeLogin`.  
  
```  
USE AdventureWorks2012;  
DROP SIGNATURE FROM HumanResources.uspUpdateEmployeeLogin   
    BY CERTIFICATE HumanResourcesDP;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Sys.crypt_properties &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-crypt-properties-transact-sql.md)   
 [Agregar firma &#40; Transact-SQL &#41;](../../t-sql/statements/add-signature-transact-sql.md)  
  
  
