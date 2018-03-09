---
title: sp_cursorfetch (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_cursorfetch
- sp_cursorfetch_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorfetch
ms.assetid: 14513c5e-5774-4e4c-92e1-75cd6985b6a3
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b9b33361094966dc180939f0cdf92ac951922139
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="spcursorfetch-transact-sql"></a>sp_cursorfetch (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Captura un búfer de una o varias filas de la base de datos. El grupo de filas de este búfer se denomina el cursor *búfer de captura*. sp_cursorfetch se invoca especificando el identificador = 7 en un paquete de flujo TDS.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_cursorfetch cursor  
    [ , fetchtype[ , rownum [ , nrows] ]]   
```  
  
## <a name="arguments"></a>Argumentos  
 *cursor*  
 Es un *controlar* valor generado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y devuelve sp_cursoropen. *cursor* es un parámetro necesario que requiere un **int** valor de entrada. Para obtener más información, vea la sección Comentarios más adelante en este tema.  
  
 *fetchType*  
 Especifica qué búfer de cursor se va a capturar. *fetchType* es un parámetro opcional que requiere uno de los siguientes valores de entrada de enteros.  
  
|Valor|Nombre|Description|  
|-----------|----------|-----------------|  
|0x0001|FIRST|Captura el primer búfer de *nrows* filas. Si *nrows* es igual a 0, el cursor se coloca antes del conjunto de resultados y no devuelve ninguna fila.|  
|0x0002|NEXT|Captura el siguiente búfer de *nrows* filas.|  
|0x0004|PREV|Captura el anterior búfer de *nrows* filas.<br /><br /> Nota: Al utilizar PREV para un cursor FORWARD_ONLY devuelve un mensaje de error porque FORWARD_ONLY solo permite el desplazamiento en una dirección.|  
|0x0008|LAST|Captura el último búfer de *nrows* filas. Si *nrows* es igual a 0, el cursor se coloca después de que el conjunto de resultados y no devuelve ninguna fila.<br /><br /> Nota: Al utilizar LAST para un cursor FORWARD_ONLY devuelve un mensaje de error porque FORWARD_ONLY solo permite el desplazamiento en una dirección.|  
|0x10|ABSOLUTE|Captura un búfer de *nrows* filas a partir de la *rownum* fila.<br /><br /> Nota: Al usar ABSOLUTE para un cursor dinámico o un cursor FORWARD_ONLY devuelve un mensaje de error porque FORWARD_ONLY solo permite el desplazamiento en una dirección.|  
|0x20|RELATIVE|Captura el búfer de *nrows* filas a partir de la fila que se especifica como el *rownum* valor de filas de la primera fila en el bloque actual. En este caso *rownum* puede ser un número negativo.<br /><br /> Nota: Al utilizar RELATIVE para un cursor FORWARD_ONLY devuelve un mensaje de error porque FORWARD_ONLY solo permite el desplazamiento en una dirección.|  
|0x80|REFRESH|Rellena el búfer a partir de las tablas subyacentes.|  
|0x100|INFO|Recupera información acerca del cursor. Esta información se devuelve mediante el uso de la *rownum* y *nrows* parámetros. Por lo tanto, cuando se especifica INFO, *rownum* y *nrows* se convierten en parámetros de salida.|  
|0x200|PREV_NOADJUST|Se utiliza como PREV. Sin embargo, si el principio del conjunto de resultados se encontrara prematuramente, los resultados podrían variar.|  
|0x400|SKIP_UPDT_CNCY|Se debe utilizar con uno de los otros *fetchtype* valores, excepto INFO.|  
  
> [!NOTE]  
>  No se admite el valor 0x40.  
  
 Para obtener más información, vea la sección Comentarios más adelante en este tema.  
  
 *ROWNUM*  
 Es un parámetro opcional que se utiliza para especificar la posición de fila para el ABSOLUTE e INFO *fetchtype* valores utilizando solo valores enteros para la entrada o salida o ambos. *ROWNUM* actúa como el desplazamiento de fila para la *fetchtype* valor relativo de bits. *ROWNUM* se omite para todos los demás valores. Para obtener más información, vea la sección Comentarios más adelante en este tema.  
  
 *nRows*  
 Es un parámetro opcional que se utiliza para especificar el número de filas que capturar. Si *nrows* no se especifica, el valor predeterminado es 20 filas. Para establecer la posición sin devolver los datos, especifique un valor de 0. Cuando *nrows* se aplica a la *fetchtype* consulta INFO, devuelve el número total de filas en la consulta.  
  
> [!NOTE]  
>  *nRows* omite la actualización *fetchtype* valor de bit.  
>   
>  Para obtener más información, vea la sección Comentarios más adelante en este tema.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 Al especificar el valor de bit INFO, los valores que se pueden devolver se muestran en las siguientes tablas.  
  
> [!NOTE]  
>  : Si no se devuelve ninguna fila, el contenido del búfer permanece tal como estaban.  
  
|*\<ROWNUM >*|Establecer en|  
|------------------|------------|  
|Si no está abierto|0|  
|Si está colocado antes del conjunto de resultados|0|  
|Si está colocado después del conjunto de resultados|-1|  
|Para los cursores KEYSET y STATIC|Número de fila absoluto de la posición actual en el conjunto de resultados|  
|Para los cursores DYNAMIC|1|  
|Para ABSOLUTE|-1 devuelve la última fila de un conjunto.<br /><br /> -2 devuelve de la segunda a la última fila de un conjunto, etc.<br /><br /> Nota: Si se solicita más de una fila que se capturan en este caso, se devuelven las dos últimas filas del conjunto de resultados.|  
  
|*\<nRows >*|Establecer en|  
|-----------------|------------|  
|Si no está abierto|0|  
|Para los cursores KEYSET y STATIC|Normalmente, el tamaño del conjunto de claves actual.<br /><br /> **– m** si el cursor está en la creación asincrónica con *m* filas encontradas en este punto.|  
|Para los cursores DYNAMIC|-1|  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="cursor-parameter"></a>Parámetro cursor  
 Antes de que se produzca ninguna operación de captura, la posición predeterminada de un cursor está antes de la primera fila del conjunto de resultados.  
  
## <a name="fetchtype-parameter"></a>Parámetro fetchtype  
 Excepción de SKIP_UPD_CNCY, la *fetchtype* valores son mutuamente excluyentes.  
  
 Cuando se especifica SKIP_UPDT_CNCY, los valores de columna de marca de tiempo no se escriben en la tabla de conjunto de claves cuando una fila se captura o actualiza. Si la fila del conjunto de claves se está actualizando, los valores de las columnas de marca de tiempo permanecen como el valor anterior. Si se inserta la fila del conjunto de claves, los valores de las columnas de marca de tiempo son indefinidos.  
  
 Para los cursores KEYSET, esto significa que la tabla del conjunto de claves tiene el conjunto de valores durante la última operación FETCH sin salto, si se realizó alguna. En otro caso, tiene el conjunto de valores durante el rellenado.  
  
 Para los cursores DYNAMIC, esto significa que si el salto se realiza con una actualización, genera los mismos resultados que KEYSET. Para cualquier otro tipo de captura, la tabla de conjunto de claves se trunca. Esto significa que se insertan las filas y que los valores de las columnas de marca de tiempo son indefinidos. Por consiguiente, al ejecutar sp_cursorfetch para los cursores DYNAMIC, evite utilizar SKIP_UPDT_CNCY para cualquier operación distinta de REFRESH.  
  
 Si se produce un error en una operación de captura porque la posición del cursor solicitada está más allá del conjunto de resultados, la posición del cursor se establece justo después de la última fila. Si se produce un error en una operación de captura porque la posición del cursor solicitada está antes del conjunto de resultados, la posición del cursor se establece antes de la primera fila.  
  
## <a name="rownum-parameter"></a>Parámetro rownum  
 Cuando usas *rownum*, el búfer se llena a partir de la fila especificada.  
  
 El *fetchtype* valor ABSOLUTO se refiere a la posición de *rownum* dentro de todo el resultado establecido. Un número negativo con ABSOLUTE especifica que la operación cuenta las filas desde el final del conjunto de resultados.  
  
 El *fetchtype* valor RELATIVE hace referencia a la posición de *rownum* en relación con la posición del cursor al principio del búfer actual. Un número negativo con RELATIVE especifica que el cursor va atrasado desde la posición del cursor actual.  
  
## <a name="nrows-parameter"></a>Parámetro nrows  
 El *fetchtype* valores REFRESH e INFO omiten este parámetro.  
  
 Cuando se especifica un *fetchtype* valor de primera que tenga un *nrow* valor de 0, el cursor se coloca antes del conjunto de resultados que no tiene filas en el búfer de captura.  
  
 Cuando se especifica un *fetchtype* valor de la última que tenga un *nrow* valor de 0, el cursor se coloca después del conjunto de resultados que no tiene filas en el búfer de captura actual.  
  
 Para el *fetchtype* valores del siguiente, PREV, ABSOLUTE, RELATIVE y PREV_NOADJUST, un *nrow* valor de 0 no es válido.  
  
## <a name="rpc-considerations"></a>Consideraciones sobre RPC  
 El estado de retorno de RPC indica si el parámetro de tamaño del conjunto de claves es final o no; es decir, si el conjunto de claves o la tabla temporal se rellenan de forma asincrónica.  
  
 El parámetro de estado de RPC se establece en uno de los valores mostrados en la siguiente tabla.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|0|El procedimiento se ejecutó correctamente.|  
|0x0001|Se produjo un error en el procedimiento.|  
|0x0002|Una captura en una dirección negativa hizo que la posición del cursor se estableciera al principio del conjunto de resultados, cuando la captura habría estado lógicamente antes que los resultados.|  
|0x10|Se cerró automáticamente un cursor de avance rápido.|  
  
 Las filas se devuelven como un conjunto de resultados típico, es decir, formato de columna (0x2a), filas (0xd1), seguido de Done (0xfd). Los tokens de metadatos se envían en el mismo formato que el especificado para sp_cursoropen, es decir, 0x81, 0xa5 y 0xa4 para los usuarios de SQL Server 7.0, etc. Los indicadores del estado de la fila se envían como columnas ocultas, similar al modo BROWSE, al final de cada fila con el nombre de columna rowstat y el tipo de datos INT4. Esta columna rowstat tiene uno de los valores que se muestran en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|0x0001|FETCH_SUCCEEDED|  
|0x0002|FETCH_MISSING|  
  
 Dado que el protocolo TDS no proporciona ninguna manera de enviar la columna de estado final sin enviar las columnas anteriores, los datos ficticios se envían para las filas que faltan (los campos que aceptan valores NULL establecidos en null, los campos de longitud fija establecidos en 0 o el valor predeterminado para esa columna, según corresponda).  
  
 El número de filas DONE siempre será cero. El mensaje DONE contiene el número de filas del conjunto de resultados real. Entre los mensajes de TDS podrían aparecer mensajes de error o informativos.  
  
 Para solicitar que los metadatos acerca de la lista de selección del cursor se devuelvan en la flujo de TDS, establezca en 1 la marca de entrada RPC RETURN_METADATA.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-prev-to-change-a-cursor-position"></a>A. Usar PREV para cambiar una posición del cursor  
 Suponga que el cursor h2 generaría un conjunto de resultados con el siguiente contenido y una posición actual como la que se muestra:  
  
```  
row 1 contents      
row 2 contents  
row 3 contents  
row 4 contents  <-- current position  
row 5 contents   
row 6 contents  
```  
  
 A continuación, una operación sp_cursorfetch PREV que tiene un *nrows* valor de 5 colocaría lógicamente el cursor dos filas antes de la primera fila del conjunto de resultados. En estos casos, el cursor se ajusta para iniciarse en la primera fila y devolver el número de filas solicitadas. Esto suele significar que devolverá las filas que estaban en el búfer de captura PRIOR.  
  
> [!NOTE]  
>  Este es el caso exacto en el que el parámetro de estado de RPC está establecido en 2.  
  
### <a name="b-using-prevnoadjust-to-return-fewer-rows-than-prev"></a>B. Usar PREV_NOADJUST para devolver menos filas que PREV  
 PREV_NOADJUST nunca incluye ninguna de las filas de la posición del cursor actual o posteriores en el bloque de filas que devuelve. En casos donde PREV devuelve las filas después de la posición actual, PREV_NOADJUST devuelve menos filas de las solicitadas en *nrows*. Dada la posición actual en el ejemplo A anterior, cuando se aplica PREV sp_cursorfetch (h2, 4, 1, 5) captura las siguientes filas:  
  
```  
row1 contents   
row2 contents  
row3 contents  
row4 contents  
row5 contents  
```  
  
 Sin embargo, cuando se aplica PREV_NOADJUST, sp_cursorfetch (h2, 512, 6, 5) captura solo las filas siguientes:  
  
```  
row1 contents   
row2 contents  
row3 contents   
```  
  
## <a name="see-also"></a>Vea también  
 [sp_cursoropen &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
