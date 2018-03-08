---
title: CRYPT_GEN_RANDOM (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CRYPT_GEN_RANDOM_TSQL
- CRYPT_GEN_RANDOM
dev_langs:
- TSQL
helpviewer_keywords:
- CRYPT_GEN_RANDOM function
ms.assetid: b74bd9d4-758e-4b94-89a0-76dcda6d8c42
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 695af04a3ee411392cf00be6b6483c9338a4c989
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="cryptgenrandom-transact-sql"></a>CRYPT_GEN_RANDOM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve un número aleatorio criptográfico generado por la API de criptografía (CAPI). La salida es un número hexadecimal del número especificado de bytes.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
CRYPT_GEN_RANDOM ( length [ , seed ] )   
```  
  
## <a name="arguments"></a>Argumentos  
*length*  
Longitud del número que se va a crear. El valor máximo es 8000. *longitud* es de tipo **int**.
  
*valor de inicialización*  
Datos opcionales que se van a utilizar como valor de inicialización aleatorio.  Debe haber al menos *longitud* bytes de datos. *valor de inicialización* es **varbinary (8000)**.
  
## <a name="returned-types"></a>Tipos devueltos  
**varbinary (8000)**
  
## <a name="permissions"></a>Permissions  
Esta función es pública y no requiere permisos especiales.
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-generating-a-random-number"></a>A. Generar un número aleatorio  
En el ejemplo siguiente se genera un número aleatorio con una longitud de 50 bytes.
  
```sql
SELECT CRYPT_GEN_RANDOM(50) ;  
```  
  
En el ejemplo siguiente se genera un número aleatorio con una longitud de 4 bytes utilizando un valor de inicialización de 4 bytes.
  
```sql
SELECT CRYPT_GEN_RANDOM(4, 0x25F18060) ;  
```  
  
## <a name="see-also"></a>Vea también
[RAND &#40; Transact-SQL &#41;](../../t-sql/functions/rand-transact-sql.md)
  
  
