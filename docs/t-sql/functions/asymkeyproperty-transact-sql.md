---
title: ASYMKEYPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ASYMKEYPROPERTY_TSQL
- ASYMKEYPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- ASYMKEYPROPERTY
ms.assetid: a30581f2-e1b1-4996-93e6-527ff96b7c42
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: de7e95ab26102c0b3bbe1e33c57ae9491a5b9a2c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "65945889"
---
# <a name="asymkeyproperty-transact-sql"></a>ASYMKEYPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Esta función devuelve las propiedades de una clave asimétrica.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
ASYMKEYPROPERTY (Key_ID , 'algorithm_desc' | 'string_sid' | 'sid')  
```  
  
## <a name="arguments"></a>Argumentos  
*Key_ID*  
Valor Key_ID de una clave asimétrica en la base de datos. Para buscar el valor Key_ID cuando solo se conoce el nombre de la clave, utilice ASYMKEY_ID. *Key_ID* tiene un tipo de datos **int**.
  
**'** algorithm_desc **'**  
Especifica que la salida devuelve la descripción del algoritmo de la clave asimétrica. Solo está disponible para las claves asimétricas creadas a partir de un módulo EKM.
  
**'** string_sid **'**  
Especifica que la salida devuelve el SID de la clave asimétrica en formato **nvarchar()** .
  
**'** sid **'**  
Especifica que la salida devuelve el SID de la clave asimétrica en formato binario.
  
## <a name="return-types"></a>Tipos de valores devueltos  
**sql_variant**
  
## <a name="permissions"></a>Permisos  
Es necesario tener los permisos apropiados sobre la clave asimétrica y que el autor de la llamada no tenga denegado el permiso VIEW sobre la clave asimétrica. Para obtener más información sobre los permisos de la clave asimétrica, vea [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md).
  
## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente se devuelven las propiedades de la clave asimétrica con un valor 256 para Key_ID.
  
```sql
SELECT   
ASYMKEYPROPERTY(256, 'algorithm_desc') AS Algorithm,  
ASYMKEYPROPERTY(256, 'string_sid') AS String_SID,  
ASYMKEYPROPERTY(256, 'sid') AS SID ;  
GO  
```  
  
## <a name="see-also"></a>Consulte también
[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
[ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)  
[DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)  
[SIGNBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/signbyasymkey-transact-sql.md)  
[VERIFYSIGNEDBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/verifysignedbyasymkey-transact-sql.md)  
[Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)  
[sys.asymmetric_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-asymmetric-keys-transact-sql.md)  
[Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)  
[ASYMKEY_ID &#40;Transact-SQL&#41;](../../t-sql/functions/asymkey-id-transact-sql.md)  
[SYMKEYPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/symkeyproperty-transact-sql.md)
  
  
