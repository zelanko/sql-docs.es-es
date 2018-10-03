---
title: Barra diagonal inversa (continuación de línea) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '\_TSQL'
- '\'
dev_langs:
- TSQL
helpviewer_keywords:
- backwhack
- backslash
- excape character
- hack character
- '\ (backslash)'
- backslant
- bash
- reverse slant
- slosh
- reversed virgule
- line continuation character
- reverse solidus
ms.assetid: c97fbb20-3d12-4d0b-9b52-62a229bc83c0
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: de0074eda569e614246bc41532dc2b0caa3c8c56
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47777103"
---
# <a name="backslash-line-continuation-transact-sql"></a>Barra diagonal inversa (continuación de línea) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

`\` divide una constante de cadena larga, de carácter o binaria, en dos o más líneas para facilitar la lectura.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
<first section of string> \  
<continued section of string>  
```  
  
## <a name="arguments"></a>Argumentos  
 \<primera sección de la cadena>  
 Es el principio de una cadena.  
  
 \<sección de continuación de la cadena>  
 Es la continuación de una cadena.  
  
## <a name="remarks"></a>Notas  
 Este comando devuelve las secciones primera y de continuación de la cadena como una cadena, sin la barra diagonal inversa.  

## <a name="examples"></a>Ejemplos  

### <a name="a-splitting-a-character-string"></a>A. División de una cadena de caracteres  

En el ejemplo siguiente se usa una barra diagonal inversa y un retorno de carro para dividir una cadena de caracteres en dos líneas.  
  
```  
SELECT 'abc\  
def' AS [ColumnResult];  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 ColumnResult  
 ------------  
 abcdef
 ```    

### <a name="b-splitting-a-binary-string"></a>B. División de una cadena binaria  

En el ejemplo siguiente se usa una barra diagonal inversa y un retorno de carro para dividir una cadena binaria en dos líneas.  

```  
SELECT 0xabc\  
def AS [ColumnResult];  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 ColumnResult  
 ------------  
 0xABCDEF
 ```    

## <a name="see-also"></a>Ver también  
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funciones integradas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [&#40;Divisió&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/divide-transact-sql.md)   
 [&#40;Asignación y División&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/divide-equals-transact-sql.md)   
 [Operadores compuestos &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  
