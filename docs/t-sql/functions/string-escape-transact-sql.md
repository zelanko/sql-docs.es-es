---
title: STRING_ESCAPE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 02/25/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STRING_ESCAPE
- STRING_ESCAPE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRING_ESCAPE function
ms.assetid: 2163bc7a-3816-4304-9c40-8954804f5465
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 41f969e292eff76c9a836ccd3177519d88e355ac
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="stringescape-transact-sql"></a>STRING_ESCAPE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Escapes de caracteres especiales en textos y devuelve el texto con caracteres de escape. **STRING_ESCAPE** es una función determinista.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
STRING_ESCAPE( text , type )  
```  
  
## <a name="arguments"></a>Argumentos  
 *text*  
 Es un **nvarchar**[expresión](../../t-sql/language-elements/expressions-transact-sql.md) expresión que representa el objeto que debe ser caracteres de escape.  
  
 *Tipo*  
 Reglas de escape que se aplicará. Actualmente el valor admitido es `'json'`.  
  
## <a name="return-types"></a>Tipos devueltos  
 **nvarchar (max)** texto con especiales de escape y caracteres de control. Actualmente **STRING_ESCAPE** sólo se puede omitir los caracteres especiales de JSON se muestra en las tablas siguientes.  
  
|Carácter especial|Secuencia codificada|  
|-----------------------|----------------------|  
|Comillas (")|\\"|  
|barra inclinada inversa (\\)|\\\|  
|barra inclinada (/)|\\/|  
|Retroceso|\b|  
|Avance de página|\f|  
|Nueva línea|\n|  
|Retorno de carro|\r|  
|Tabulación horizontal|\t|  
  
|Carácter de control|Secuencia codificada|  
|-----------------------|----------------------|  
|CHAR(0)|\u0000|  
|CHAR(1)|\u0001|  
|...|...|  
|CHAR(31)|\u001f|  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a--escape-text-according-to-the-json-formatting-rules"></a>A.  Escape texto según la reglas de formato de JSON  
 La siguiente consulta convierte caracteres especiales mediante las reglas JSON y devuelve el texto de escape.  
  
```  
SELECT STRING_ESCAPE('\   /  
\\    "     ', 'json') AS escapedText;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
escapedText  
-------------------------------------------------------------  
\\\t\/\n\\\\\t\"\t
```  
  
### <a name="b-format-json-object"></a>B. Objeto JSON de formato  
 La siguiente consulta crea texto JSON a partir de las variables de cadena y el número y convierte cualquier carácter especial de JSON en variables.  
  
```  
SET @json = FORMATMESSAGE('{ "id": %d,"name": "%s", "surname": "%s" }',   
    17, STRING_ESCAPE(@name,'json'), STRING_ESCAPE(@surname,'json') );  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de cadena &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [SUBCADENA &#40; Transact-SQL &#41;](../../t-sql/functions/substring-transact-sql.md)  
  
  

