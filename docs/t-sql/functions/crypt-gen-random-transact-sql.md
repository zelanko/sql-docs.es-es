---
title: CRYPT_GEN_RANDOM (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CRYPT_GEN_RANDOM_TSQL
- CRYPT_GEN_RANDOM
dev_langs:
- TSQL
helpviewer_keywords:
- CRYPT_GEN_RANDOM function
ms.assetid: b74bd9d4-758e-4b94-89a0-76dcda6d8c42
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: a0e2081eef43cdc892e3b48457c10f9e935c5d0d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85732477"
---
# <a name="crypt_gen_random-transact-sql"></a>CRYPT_GEN_RANDOM (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Esta función devuelve un número criptográfico y aleatorio, generado por Crypto API (CAPI). `CRYPT_GEN_RANDOM` devuelve un número hexadecimal con una longitud de un número especificado de bytes.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```syntaxsql
CRYPT_GEN_RANDOM ( length [ , seed ] )   
```  
  
## <a name="arguments"></a>Argumentos  
*length*  
La longitud, en bytes, del número que `CRYPT_GEN_RANDOM` va a crear. El argumento *length*  tiene un tipo de datos **int** y un rango de valores entre 1 y 8000. `CRYPT_GEN_RANDOM` devuelve NULL para un valor **int** fuera de este rango. 
  
*seed*  
Un número hexadecimal opcional, para su uso como un valor de inicialización aleatorio. La longitud de *seed* debe coincidir con el valor del argumento *length*. El argumento *seed* tiene un tipo de datos **varbinario(8000)** .
  
## <a name="returned-types"></a>Tipos devueltos  
**varbinary(8000)**
  
## <a name="permissions"></a>Permisos  
Esta función es pública y no requiere permisos especiales.
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-generating-a-random-number"></a>A. Generar un número aleatorio  
En este ejemplo se genera un número aleatorio con una longitud de 50 bytes:
  
```sql
SELECT CRYPT_GEN_RANDOM(50) ;  
```  
  
En este ejemplo se genera un número aleatorio con una longitud de 4 bytes utilizando un valor de inicialización de 4 bytes:
  
```sql
SELECT CRYPT_GEN_RANDOM(4, 0x25F18060) ;  
```  
  
## <a name="see-also"></a>Consulte también
[RAND &#40;Transact-SQL&#41;](../../t-sql/functions/rand-transact-sql.md)
  
  
