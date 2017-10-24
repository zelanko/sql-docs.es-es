---
title: TEXTPTR (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TEXTPTR_TSQL
- TEXTPTR
dev_langs:
- TSQL
helpviewer_keywords:
- TEXTPTR function
- viewing text pointer values
- text-pointer values
- displaying text pointer values
ms.assetid: 2672b8cb-f747-46f3-9358-9b49b3583b8e
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 84eaad80eff48689f91ab2679611d6eab6b2ce4d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="text-and-image-functions---textptr-transact-sql"></a>Funciones de texto e imagen: TEXTPTR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El puntero de texto devuelve un valor que corresponde a un **texto**, **ntext**, o **imagen** columna en **varbinary** formato. El valor del puntero de texto devuelto se puede utilizar en las instrucciones READTEXT, WRITETEXT y UPDATE.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] No hay ninguna funcionalidad alternativa disponible.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
TEXTPTR ( column )  
```  
  
## <a name="arguments"></a>Argumentos  
 *columna*  
 Es el **texto**, **ntext**, o **imagen** columna que va a utilizar.  
  
## <a name="return-types"></a>Tipos devueltos  
 **varbinary**  
  
## <a name="remarks"></a>Comentarios  
 En las tablas con texto consecutivo, TEXTPTR devuelve un controlador para el texto que se va a procesar. Es posible obtener un puntero de texto válido aunque el valor del texto sea NULL.  
  
 La función TEXTPTR no se puede utilizar en columnas de vistas. Solo se puede utilizar en columnas de tablas. Para usar la función TEXTPTR en una columna de una vista, debe establecer el nivel de compatibilidad en 80 mediante [nivel de compatibilidad de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md). Si la tabla no tiene texto de fila y una **texto**, **ntext**, o **imagen** columna no se ha inicializado mediante una instrucción UPDATETEXT, TEXTPTR devuelve un puntero nulo.  
  
 Utilice TEXTVALID para comprobar si un puntero de texto existe. No es posible utilizar UPDATETEXT, WRITETEXT o READTEXT sin un puntero de texto válido.  
  
 Estas funciones e instrucciones también son útiles cuando se trabaja con **texto**, **ntext**, y **imagen** datos.  
  
|Función o instrucción|Description|  
|---------------------------|-----------------|  
|PATINDEX**('***patrón %***',** *expresión***)**|Devuelve la posición del carácter de una cadena de caracteres especificada en **texto** o **ntext** columnas.|  
|DATALENGTH**(***expresión***)**|Devuelve la longitud de datos en **texto**, **ntext**, y **imagen** columnas.|  
|SET TEXTSIZE|Devuelve el límite, en bytes, de la **texto**, **ntext**, o **imagen** datos que se devolverán con una instrucción SELECT.|  
|SUBCADENA**(***text_column*, *iniciar*, *longitud***)**|Devuelve un **varchar** cadena especificada por el objeto *iniciar* desplazamiento y *longitud*. La longitud debe ser inferior a 8 KB.|  
  
## <a name="examples"></a>Ejemplos  
  
> [!NOTE]  
>  Para ejecutar los ejemplos siguientes, debe instalar la **pubs** base de datos.  
  
### <a name="a-using-textptr"></a>A. Usar TEXTPTR  
 En el ejemplo siguiente se usa el `TEXTPTR` función para buscar la **imagen** columna `logo` asociada `New Moon Books` en el `pub_info` tabla de la `pubs` base de datos. El puntero de texto se coloca en la variable local `@ptrval.`  
  
```  
USE pubs;  
GO  
DECLARE @ptrval varbinary(16);  
SELECT @ptrval = TEXTPTR(logo)  
FROM pub_info pr, publishers p  
WHERE p.pub_id = pr.pub_id   
   AND p.pub_name = 'New Moon Books';  
GO  
```  
  
### <a name="b-using-textptr-with-in-row-text"></a>B. Usar TEXTPTR con texto consecutivo  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el puntero de texto consecutivo debe utilizarse dentro de una transacción, como se muestra en el ejemplo siguiente.  
  
```  
CREATE TABLE t1 (c1 int, c2 text);  
EXEC sp_tableoption 't1', 'text in row', 'on';  
INSERT t1 VALUES ('1', 'This is text.');  
GO  
BEGIN TRAN;  
   DECLARE @ptrval VARBINARY(16);  
   SELECT @ptrval = TEXTPTR(c2)  
   FROM t1  
   WHERE c1 = 1;  
   READTEXT t1.c2 @ptrval 0 1;  
COMMIT;  
```  
  
### <a name="c-returning-text-data"></a>C. Devolver datos de texto  
 En el ejemplo siguiente se seleccionan la columna `pub_id` y el puntero de texto de 16 bits de la columna `pr_info` de la tabla `pub_info`.  
  
```  
USE pubs;  
GO  
SELECT pub_id, TEXTPTR(pr_info)  
FROM pub_info  
ORDER BY pub_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pub_id                                      
------ ----------------------------------   
0736   0x6c0000000000feffb801000001000100   
0877   0x6d0000000000feffb801000001000300   
1389   0x6e0000000000feffb801000001000500   
1622   0x700000000000feffb801000001000900   
1756   0x710000000000feffb801000001000b00   
9901   0x720000000000feffb801000001000d00   
9952   0x6f0000000000feffb801000001000700   
9999   0x730000000000feffb801000001000f00   
  
(8 row(s) affected)  
```  
  
 En el ejemplo siguiente se muestra cómo devolver los primeros `8000` bytes de texto sin utilizar TEXTPTR.  
  
```  
USE pubs;  
GO  
SET TEXTSIZE 8000;  
SELECT pub_id, pr_info  
FROM pub_info  
ORDER BY pub_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pub_id pr_info                                                                                                                                                                                                                                                           
------ -----------------------------------------------------------------  
0736   New Moon Books (NMB) has just released another top ten publication. With the latest publication this makes NMB the hottest new publisher of the year!                                                                                                             
0877   This is sample text data for Binnet & Hardley, publisher 0877 in the pubs database. Binnet & Hardley is located in Washington, D.C.  
  
This is sample text data for Binnet & Hardley, publisher 0877 in the pubs database. Binnet & Hardley is located in Washi   
1389   This is sample text data for Algodata Infosystems, publisher 1389 in the pubs database. Algodata Infosystems is located in Berkeley, California.  
  
9999   This is sample text data for Lucerne Publishing, publisher 9999 in the pubs database. Lucerne publishing is located in Paris, France.  
  
This is sample text data for Lucerne Publishing, publisher 9999 in the pubs database. Lucerne publishing is located in   
  
(8 row(s) affected)  
```  
  
### <a name="d-returning-specific-text-data"></a>D. Devolver datos de texto específicos  
 En el ejemplo siguiente se encuentra el `text` columna (`pr_info`) asociado a `pub_id``0736` en el `pub_info` tabla de la `pubs` base de datos. Primero se declara la variable local `@val`. A continuación, el puntero de texto (una cadena binaria de tipo long) se coloca en `@val` y se suministra como parámetro a la instrucción `READTEXT`. De esta forma, se devuelven 10 bytes a partir del quinto byte (el desplazamiento es 4).  
  
```  
USE pubs;  
GO  
DECLARE @val varbinary(16);  
SELECT @val = TEXTPTR(pr_info)   
FROM pub_info  
WHERE pub_id = '0736';  
READTEXT pub_info.pr_info @val 4 10;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pr_info                                                                                                                                                                                                                                                           
-----------------------------------------------------------------------  
 is sample  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Vea también  
 [DATALENGTH &#40; Transact-SQL &#41;](../../t-sql/functions/datalength-transact-sql.md)   
 [PATINDEX &#40; Transact-SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)   
 [READTEXT &#40; Transact-SQL &#41;](../../t-sql/queries/readtext-transact-sql.md)   
 [SET TEXTSIZE &#40; Transact-SQL &#41;](../../t-sql/statements/set-textsize-transact-sql.md)   
 [Texto y funciones de imagen &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)   
 [UPDATETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)   
 [WRITETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)  
  
  

