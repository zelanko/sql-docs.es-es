---
title: sp_cursor (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_cursor_TSQL
- sp_cursor
dev_langs: TSQL
helpviewer_keywords: sp_cursor
ms.assetid: 41ade0ca-5f11-469d-bd4d-c8302ccd93b3
caps.latest.revision: "10"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e85732afe35198cea86a605dfde8396b013842dc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spcursor-transact-sql"></a>sp_cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Solicita actualizaciones posicionadas. Este procedimiento realiza las operaciones en una o más filas dentro del búfer de captura de un cursor. sp_cursor se invoca especificando el identificador igual a 1 en un paquete de flujo TDS.  
  
||  
|-|  
|**Se aplica a**: SQL Server ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_cursor  cursor, optype, rownum, table  
    [ , value[...n]]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *cursor*  
 El identificador de cursor. *cursor* es un parámetro necesario que requiere un **int** valor de entrada. *cursor* es el *controlar* valor generados por SQL Server y devuelto por el procedimiento sp_cursoropen.  
  
 *optype*  
 Es un parámetro necesario que designa qué operación realizará el cursor. *optype* requiere uno de los siguientes **int** valores de entrada.  
  
|Valor|Nombre|Description|  
|-----------|----------|-----------------|  
|0X0001|UPDATE|Se usa para actualizar una o varias filas en el búfer de captura.  Las filas especificadas en *rownum* se vuelve a acceder y se actualizan.|  
|0x0002|DELETE|Se usa para eliminar una o varias filas en el búfer de captura. Las filas especificadas en *rownum* volver a tiene acceso y eliminar.|  
|0X0004|INSERT|Inserta los datos sin generar una SQL **insertar** instrucción.|  
|0X0008|REFRESH|Se usa para rellenar el búfer a partir de las tablas subyacentes y se puede usar para actualizar la fila si una actualización o eliminación no puede realizarse debido a un control de simultaneidad optimista o después de una operación UPDATE.|  
|0X10|LOCK|Hace que un servidor SQL U-bloqueo que se adquiera en la página que contiene la fila especificada. Este bloqueo es compatible con los bloqueos S. No es compatible con los bloqueos X ni U. Se puede usar para implementar el bloqueo a corto plazo.|  
|0X20|SETPOSITION|Se utiliza únicamente cuando el programa se va a emitir un servidor SQL siguientes coloca la instrucción DELETE o UPDATE.|  
|0X40|ABSOLUTE|Solo se puede usar junto con UPDATE o DELETE.  ABSOLUTE solo se emplea con cursores KEYSET (se omite para los cursores DYNAMIC y los cursores STATIC no se pueden actualizar).<br /><br /> Nota: Si se especifica ABSOLUTE en una fila en el conjunto de claves que no se ha capturado, la operación puede producir un error en la comprobación de simultaneidad y el resultado devuelto no se puede garantizar.|  
  
 *ROWNUM*  
 Especifica con cuál de las filas del búfer de captura operará el cursor, cuál actualizará o cuál eliminará.  
  
> [!NOTE]  
>  Esto no afecta al punto inicial de ninguna operación de captura RELATIVE, NEXT o PREVIOUS, ni a las actualizaciones ni eliminaciones realizadas con sp_cursor.  
  
 *ROWNUM* es un parámetro necesario que requiere un **int** valor de entrada.  
  
 1  
 Indica la primera fila del búfer de captura.  
  
 2  
 Indica la segunda fila del búfer de captura.  
  
 3, 4, 5  
 Indica la tercera fila, etc.  
  
 n  
 Indica la enésima fila del búfer de captura.  
  
 0  
 Indica todas las filas del búfer de captura.  
  
> [!NOTE]  
>  Solo es válida para su uso con UPDATE, DELETE, actualización o bloqueo *optype* valores.  
  
 *table*  
 Nombre de la tabla que identifica la tabla que *optype* se aplica a cuando la definición de cursor implica una unión o devuelven nombres de columna ambigua la *valor* parámetro. Si no se designa ninguna tabla específica, el valor predeterminado es la primera tabla de la cláusula FROM. *tabla* es un parámetro opcional que requiere un valor de entrada de cadena. La cadena se puede especificar como cualquier tipo de datos UNICODE o carácter. *tabla* puede ser un nombre de tabla de varias partes.  
  
 *value*  
 Se usa para insertar o actualizar valores. El *valor* solo se usa el parámetro de cadena con UPDATE e INSERT *optype* valores. La cadena se puede especificar como cualquier tipo de datos UNICODE o carácter.  
  
> [!NOTE]  
>  Los nombres de parámetro para *valor* se puede asignar el usuario.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 Cuando se usa una llamada RPC, una operación DELETE o UPDATE posicionada con un número de búfer 0 devolverá un mensaje DONE con un *rowcount* de 0 (error) o 1 (correcto) para cada fila del búfer de captura.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="optype-parameter"></a>Parámetro optype  
 Con la excepción de las combinaciones de SETPOSITION con UPDATE, DELETE, actualización o bloqueo; ABSOLUTA con UPDATE o DELETE, o la *optype* valores son mutuamente excluyentes.  
  
 La cláusula SET del valor UPDATE se construye a partir del *valor* parámetro.  
  
 Una ventaja de utilizar la instrucción INSERT *optype* valor es que puede evitar la conversión de datos que no son caracteres en el formato de caracteres para las inserciones. Los valores se especifican de la misma manera que para UPDATE. Si alguna columna necesaria no está incluida, se produce un error en INSERT.  
  
-   El valor SETPOSITION no afecta al punto inicial de ninguna operación de captura RELATIVE, NEXT o PREVIOUS, ni hace ninguna actualización ni eliminación que se efectúe con la interfaz sp_cursor. Cualquier número que no especifique una fila en el búfer de captura hará que la posición se establezca en 1 y no se devuelva ningún error. Una vez ejecutada, la posición permanece en vigor hasta la siguiente operación sp_cursorfetch, T-SQL **capturar** operación, o sp_cursor SETPOSITION a través del mismo cursor. La siguiente operación sp_cursorfetch establecerá la posición del cursor en la primera fila del nuevo búfer de captura, mientras que otras llamadas del cursor no afectarán al valor de la posición. Una cláusula OR con REFRESH, UPDATE, DELETE o LOCK puede vincular SETPOSITION para establecer el valor de la posición en la última fila modificada.  
  
 Si no se especifica una fila del búfer de captura a través de la *rownum* parámetro, la posición se establecerá en 1, y se devolverá ningún error. Una vez establecida la posición, permanece en vigor hasta que se realiza la siguiente operación sp_cursorfetch, FETCH de T-SQL o sp_cursor SETPOSITION en el mismo cursor.  
  
 SETPOSITION puede vincularse con cualquier cláusula REFRESH, UPDATE, DELETE o LOCK para establecer la posición del cursor en la última fila modificada.  
  
## <a name="rownum-parameter"></a>Parámetro rownum  
 Si se especifica, el *rownum* parámetro se puede interpretar como el número de fila en el conjunto de claves en lugar del número de fila en el búfer de captura. El usuario es responsable de asegurarse de que el control de simultaneidad se mantenga. Esto significa que para los cursores SCROLL_LOCKS, debe mantener independientemente un bloqueo en la fila dada (esto se puede hacer a través de una transacción). En el caso de los cursores optimistas, debe haber capturado previamente la fila para realizar esta operación.  
  
## <a name="table-parameter"></a>Parámetro table  
 Si el *optype* valor es UPDATE o INSERT y una instrucción de inserción o actualización completa se envía como el *valor* parámetro, el valor especificado para *tabla* se omite.  
  
> [!NOTE]  
>  En relación con las vistas, solo se puede modificar una tabla que participa en la vista. El *valor* nombres de columna de parámetro deben reflejar los nombres de columna en la vista, pero puede ser el nombre de la tabla de la tabla base subyacente (en cuyo caso sp_cursor sustituirá al nombre de vista).  
  
## <a name="value-parameter"></a>Parámetro value  
 Hay dos alternativas a las reglas para usar *valor* como se mencionó anteriormente en la sección argumentos:  
  
1.  Puede usar un nombre que sea ' @' a anteponer al nombre de la columna en la lista de selección para cualquier denominado *valor* parámetros. Una ventaja de esta alternativa es que la conversión de datos puede no ser necesaria.  
  
2.  Usar un parámetro para enviar una instrucción INSERT o UPDATE completa, o use varios parámetros para enviar partes de una instrucción INSERT o UPDATE que SQL Server, a continuación, se compilará en una instrucción completa. Puede encontrar ejemplos de esto en la sección Ejemplos, posteriormente en este tema.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="alternative-value-parameter-uses"></a>Usos alternativos del parámetro value  
 Para UPDATE:  
  
 Cuando se utiliza un solo parámetro, se puede enviar una instrucción UPDATE con la siguiente sintaxis:  
  
 `[ [ UPDATE <table name> ] SET ] {<column name> = expression} [,…n]`  
  
> [!NOTE]  
>  Si actualización \<nombre de tabla > se especifica, cualquier valor especificado para la *tabla* parámetro se omitirá.  
  
 Cuando se utilizan varios parámetros, el primero debe ser una cadena con el siguiente formato:  
  
 `[ SET ] <column name> = expression  [,...n]`  
  
 y los parámetros subsiguientes deben estar en el formato:  
  
 `<column name> = expression  [,...n]`  
  
 En este caso, el \<nombre de tabla > en la actualización construida instrucción es el especificado o su valor predeterminado por el *tabla* parámetro.  
  
 Para INSERT:  
  
 Cuando se utiliza un solo parámetro, se puede enviar una instrucción INSERT con la siguiente sintaxis:  
  
 `[ [ INSERT [INTO] <table name> ] VALUES ] ( <expression> [,...n] )`  
  
> [!NOTE]  
>  Si INSERT  *\<nombre de tabla >* se especifica, cualquier valor especificado para la *tabla* parámetro se omitirá.  
  
 Cuando se utilizan varios parámetros, el primero debe ser una cadena con el siguiente formato:  
  
 `[ VALUES ( ] <expression>  [,...n]`  
  
 y los parámetros subsiguientes deben estar en el formato:  
  
 `expression [,...n]`  
  
 excepto cuando se especificó VALUES, en cuyo caso debe haber un carácter ")" final después de la última expresión. En este caso, el  *\<nombre de tabla >* en Update construida instrucción es el especificado o su valor predeterminado por el *tabla* parámetro.  
  
> [!NOTE]  
>  Es posible enviar un parámetro como un parámetro con nombre, es decir "`@VALUES`". En este caso no se pueden usar otros parámetros con nombre.  
  
## <a name="see-also"></a>Vea también  
 [sp_cursoropen &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorfetch &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
