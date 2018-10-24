---
title: TEXTVALID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TEXTVALID_TSQL
- TEXTVALID
dev_langs:
- TSQL
helpviewer_keywords:
- invalid text pointers [SQL Server]
- valid text pointers [SQL Server]
- TEXTVALID function
- checking text pointers
- text-pointer values
- verifying text pointers
ms.assetid: 9411c349-b59b-4740-a270-92f91d81ad23
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 01e165cf75dbb411507ead1bab3728cf4e142df9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47799733"
---
# <a name="text-and-image-functions---textvalid-transact-sql"></a>Funciones de texto e imagen - TEXTVALID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Una función de tipo **text**, **ntext** o **image** que comprueba la validez de un puntero de texto específico.  
  
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
  
 *column*  
 Es el nombre de la columna que se va a utilizar.  
  
 *text_ptr*  
 Es el puntero de texto que se va a comprobar.  
  
## <a name="return-types"></a>Tipos devueltos  
 **int**  
  
## <a name="remarks"></a>Notas  
 Devuelve 1 si el puntero es válido y 0 si no lo es. Observe que el identificador de la columna de tipo **text** debe incluir el nombre de la tabla. No es posible utilizar UPDATETEXT, WRITETEXT o READTEXT sin un puntero de texto válido.  
  
 Estas funciones e instrucciones son también útiles cuando se trabaja con datos de tipo **text**, **ntext** e **image**.  
  
|Función o instrucción|Descripción|  
|---------------------------|-----------------|  
|PATINDEX **(**'_%pattern%_'**,** _expression_**)**|Devuelve la posición de carácter de una cadena de caracteres especificada en columnas de tipo **text** y **ntext**.|  
|DATALENGTH **(**_expression_**)**|Devuelve la longitud de datos en columnas **text**, **ntext** e **image**.|  
|SET TEXTSIZE|Devuelve el límite en bytes de los datos de tipo **text**, **ntext** o **image** que se devuelven con una instrucción SELECT.|  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se informa acerca de si existe un puntero de texto válido para cada valor de la columna `logo` de la tabla `pub_info`.  
  
> [!NOTE]  
>  Para ejecutar este ejemplo, debe instalar la base de datos **pubs**.  
  
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
  
## <a name="see-also"></a>Ver también  
 [DATALENGTH &#40;Transact-SQL&#41;](../../t-sql/functions/datalength-transact-sql.md)   
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)   
 [SET TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/statements/set-textsize-transact-sql.md)   
 [Funciones de texto e imagen &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)   
 [TEXTPTR &#40;Transact-SQL&#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)  
  
  
