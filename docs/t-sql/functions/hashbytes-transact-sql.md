---
title: HASHBYTES (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- HASHBYTES_TSQL
- HASHBYTES
dev_langs:
- TSQL
helpviewer_keywords:
- hash input
- HASHBYTES
ms.assetid: 0ea6a4d1-313e-4f70-b939-dd2cd570f6d6
caps.latest.revision: 38
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 863cba3558cfe2e6ab070a7c4ef85091cdbf74bc
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43080394"
---
# <a name="hashbytes-transact-sql"></a>HASHBYTES (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve el hash MD2, MD4, MD5, SHA, SHA1 o SHA2 de su entrada en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HASHBYTES ( '<algorithm>', { @input | 'input' } )  
  
<algorithm>::= MD2 | MD4 | MD5 | SHA | SHA1 | SHA2_256 | SHA2_512   
```  
  
## <a name="arguments"></a>Argumentos  
 **'**\<algorithm>**'**  
 Identifica el algoritmo hash que se va a utilizar para realizar el hash de la entrada. Es un argumento requerido y no tiene valor predeterminado. Las comillas simples son necesarias. A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], todos los algoritmos están en desuso, salvo SHA2_256 y SHA2_512. Los algoritmos antiguos (no recomendados) seguirán funcionando, pero generarán un evento de desuso.  
  
 **@input**  
 Especifica una variable que contiene los datos en los que se va a realizar el hash. **@input** es **varchar**, **nvarchar** o **varbinary**.  
  
 **'** *input* **'**  
 Especifica una expresión que se evalúa como un carácter o una cadena binaria que se va a aplicar el algoritmo hash.  
  
 La salida se ajusta al algoritmo estándar: 128 bits (16 bytes) para MD2, MD4 y MD5; 160 bits (20 bytes) para SHA y SHA1; 256 bits (32 bytes) para SHA2_256 y 512 bits (64 bytes) para SHA2_512.  
  
**Se aplica a**: de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 En [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones anteriores, los valores de entrada permitidos tienen un límite de 8000 bytes.  
  
## <a name="return-value"></a>Valor devuelto  
 **varbinary** (máximo de 8000 bytes)  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-return-the-hash-of-a-variable"></a>A. Devolver el valor hash de una variable  
 En el siguiente ejemplo se devuelve el hash `SHA1` de los datos **nvarchar** almacenados en la variable `@HashThis`.  
  
```  
DECLARE @HashThis nvarchar(4000);  
SET @HashThis = CONVERT(nvarchar(4000),'dslfdkjLK85kldhnv$n000#knf');  
SELECT HASHBYTES('SHA1', @HashThis);  
  
```  
  
### <a name="b-return-the-hash-of-a-table-column"></a>B. Devolver el valor hash de una columna de tabla  
 En el ejemplo siguiente se devuelve el valor hash SHA1 de los valores de la columna `c1` de la tabla `Test1`.  
  
```  
CREATE TABLE dbo.Test1 (c1 nvarchar(50));  
INSERT dbo.Test1 VALUES ('This is a test.');  
INSERT dbo.Test1 VALUES ('This is test 2.');  
SELECT HASHBYTES('SHA1', c1) FROM dbo.Test1;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
-------------------------------------------  
0x0E7AAB0B4FF0FD2DFB4F0233E2EE7A26CD08F173  
0xF643A82F948DEFB922B12E50B950CEE130A934D6  
  
(2 row(s) affected)  
  
```  
  
## <a name="see-also"></a>Ver también  
 [Elegir un algoritmo de cifrado](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
  
