---
title: TEXTVALID (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TEXTVALID_TSQL
- TEXTVALID
dev_langs: TSQL
helpviewer_keywords:
- invalid text pointers [SQL Server]
- valid text pointers [SQL Server]
- TEXTVALID function
- checking text pointers
- text-pointer values
- verifying text pointers
ms.assetid: 9411c349-b59b-4740-a270-92f91d81ad23
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d64916b441c65dc00e0e387e08c2967124721514
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="text-and-image-functions---textvalid-transact-sql"></a>Texto e imagen funciones - TEXTVALID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A **texto**, **ntext**, o **imagen** función que comprueba si un puntero de texto específica es válido.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] No hay ninguna funcionalidad alternativa disponible.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
TEXTVALID ( 'table.column' ,text_ ptr )  
```  
  
## <a name="arguments"></a>Argumentos  
 *table*  
 Es el nombre de la tabla que se va a utilizar.  
  
 *columna*  
 Es el nombre de la columna que se va a utilizar.  
  
 *text_ptr*  
 Es el puntero de texto que se va a comprobar.  
  
## <a name="return-types"></a>Tipos devueltos  
 **int**  
  
## <a name="remarks"></a>Comentarios  
 Devuelve 1 si el puntero es válido y 0 si no lo es. Tenga en cuenta que el identificador de la **texto** columna debe incluir el nombre de tabla. No es posible utilizar UPDATETEXT, WRITETEXT o READTEXT sin un puntero de texto válido.  
  
 Las siguientes funciones e instrucciones también son útiles cuando se trabaja con **texto**, **ntext**, y **imagen** datos.  
  
|Función o instrucción|Description|  
|---------------------------|-----------------|  
|PATINDEX**(**'*patrón %**'***,** *expresión***)**|Devuelve la posición del carácter de una cadena de caracteres especificada en **texto** y **ntext** columnas.|  
|DATALENGTH**(***expresión***)**|Devuelve la longitud de datos en **texto**, **ntext**, y **imagen** columnas.|  
|SET TEXTSIZE|Devuelve el límite, en bytes, de la **texto**, **ntext**, o **imagen** datos que se devolverán con una instrucción SELECT.|  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se informa acerca de si existe un puntero de texto válido para cada valor de la columna `logo` de la tabla `pub_info`.  
  
> [!NOTE]  
>  Para ejecutar este ejemplo, debe instalar la **pubs** base de datos.  
  
```  
USE pubs;  
GO  
SELECT pub_id, 'Valid (if 1) Text data'   
   = TEXTVALID ('pub_info.logo', TEXTPTR(logo))   
FROM pub_info  
ORDER BY pub_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pub_id Valid (if 1) Text data   
------ ----------------------   
0736   1                        
0877   1                        
1389   1                        
1622   1                        
1756   1                        
9901   1                        
9952   1                        
9999   1                        
  
(8 row(s) affected)  
```  
  
## <a name="see-also"></a>Vea también  
 [DATALENGTH &#40; Transact-SQL &#41;](../../t-sql/functions/datalength-transact-sql.md)   
 [PATINDEX &#40; Transact-SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)   
 [SET TEXTSIZE &#40; Transact-SQL &#41;](../../t-sql/statements/set-textsize-transact-sql.md)   
 [Texto y funciones de imagen &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)   
 [TEXTPTR &#40; Transact-SQL &#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)  
  
  
