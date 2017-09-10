---
title: (Barra diagonal inversa) (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2008)
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
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 011025d20b6341b9fa43b25f6c14c91a135a6ffa
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="sql-server-utilities-statements---backslash"></a>Instrucciones de utilidades SQL Server - barra diagonal inversa
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Proporciona los comandos que no son [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones, pero son reconocidos por el **sqlcmd** y **osql** utilidades y [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Editor de código. Estos comandos se pueden usar para facilitar la legibilidad y la ejecución de lotes y scripts.  
  
\ divide una cadena larga constante en dos o más líneas para mejorar la legibilidad.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
<first section of string> \  
<continued section of string>  
```  
  
## <a name="arguments"></a>Argumentos  
 \<primera sección de cadena >  
 Es el principio de una cadena.  
  
 \<sigue la sección de cadena >  
 Es la continuación de una cadena.  
  
## <a name="remarks"></a>Comentarios  
 Este comando devuelve las secciones primera y de continuación de la cadena como una cadena, sin la barra diagonal inversa.  
  
 La barra diagonal inversa no es una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)]. Es un comando reconocido por el **sqlcmd** y **osql** utilidades y [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Editor de código.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa una barra diagonal inversa y un retorno de carro para dividir la cadena en dos líneas.  
  
```  
SELECT 'abc\  
def' AS ColumnResult;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 ColumnResult  
 ------------  
 abcdef
 ```    
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funciones integradas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operadores & #40; Transact-SQL & #41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [& #40; división & #41; & #40; Transact-SQL & #41;](../../t-sql/language-elements/divide-transact-sql.md)   
 [& #40; dividir es igual a & #41; & #40; Transact-SQL & #41;](../../t-sql/language-elements/divide-equals-transact-sql.md)   
 [Compuesta operadores & #40; Transact-SQL & #41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  

