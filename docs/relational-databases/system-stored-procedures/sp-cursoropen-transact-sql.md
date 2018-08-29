---
title: sp_cursoropen (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cursoropen
- sp_cursoropen_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursoropen
ms.assetid: 16462ede-4393-4293-a598-ca88c48ca70b
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c10ba380b31a2d8169dcf0a57de15418db059eac
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43028164"
---
# <a name="spcursoropen-transact-sql"></a>sp_cursoropen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Abre un cursor. sp_cursoropen define la instrucción SQL asociada con el cursor y las opciones de cursor y, a continuación, rellena el cursor. sp_cursoropen es equivalente a la combinación de la [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones DECLARE_CURSOR y OPEN. Este procedimiento se invoca especificando el identificador 2 en un paquete de flujo TDS.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_cursoropen cursor OUTPUT, stmt  
    [, scrollopt[ OUTPUT ] [ , ccopt[ OUTPUT ]  
    [ ,rowcount OUTPUT [ ,boundparam][,...n]]] ]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *cursor*  
 Un identificador del cursor generado por SQL Server. *cursor* es un *controlar* valor que se debe proporcionar en todos los procedimientos subsiguientes que impliquen al cursor, como sp_cursorfetch. *cursor* es un parámetro necesario con un **int** valor devuelto.  
  
 *cursor* permite que varios cursores estén activos en una conexión de base de datos única.  
  
 *stmt*  
 Es un parámetro necesario que define el conjunto de resultados del cursor. Cualquier cadena de consulta válida (sintaxis y enlace) de cualquier tipo de cadena (independiente de Unicode, tamaño, etc.) puede servir como válido *stmt* tipo de valor.  
  
 *scrollopt*  
 Opción de desplazamiento. *scrollopt* es un parámetro opcional que requiere uno de los siguientes **int** valores de entrada.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
|0x10|FAST_FORWARD|  
|0x1000|PARAMETERIZED_STMT|  
|0x2000|AUTO_FETCH|  
|0x4000|AUTO_CLOSE|  
|0x8000|CHECK_ACCEPTED_TYPES|  
|0x10000|KEYSET_ACCEPTABLE|  
|0x20000|DYNAMIC_ACCEPTABLE|  
|0x40000|FORWARD_ONLY_ACCEPTABLE|  
|0x80000|STATIC_ACCEPTABLE|  
|0x100000|FAST_FORWARD_ACCEPTABLE|  
  
 Debido a la posibilidad de que el valor solicitado no es adecuado para el cursor definido por *stmt*, este parámetro actúa tanto de entrada y salida. En casos como este, SQL Server asigna un valor adecuado.  
  
 *ccopt*  
 Opción de control de simultaneidad. *ccopt* es un parámetro opcional que requiere uno de los siguientes **int** valores de entrada.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS (conocido anteriormente como LOCKCC)|  
|0x0004|**OPTIMISTA** (conocido anteriormente como OPTCC)|  
|0x0008|OPTIMISTIC (conocido anteriormente como OPTCCVAL)|  
|0x2000|ALLOW_DIRECT|  
|0x4000|UPDT_IN_PLACE|  
|0x8000|CHECK_ACCEPTED_OPTS|  
|0x10000|READ_ONLY_ACCEPTABLE|  
|0x20000|SCROLL_LOCKS_ACCEPTABLE|  
|0x40000|OPTIMISTIC_ACCEPTABLE|  
|0x80000|OPTIMISITC_ACCEPTABLE|  
  
 Igual que con *scrollopt*, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede invalidar solicitado *ccopt* valores.  
  
 *recuento de filas*  
 Número de filas del búfer de captura que se usan con AUTO_FETCH. El valor predeterminado es 20 filas. *recuento de filas* tiene un comportamiento diferente cuando se asigna como un valor de entrada frente a un valor devuelto.  
  
|Como valor de entrada|Como valor devuelto|  
|--------------------|---------------------|  
|Cuando el AUTO_FETCH *scrollopt* se especifica el valor *rowcount* representa el número de filas que se va a colocar en el búfer de captura.<br /><br /> Nota: > 0 es un valor válido cuando se especifica AUTO_FETCH, pero en caso contrario, se omite.|Representa el número de filas del resultado de conjunto, excepto cuando la *scrollopt* valor AUTO_FETCH.|  
  
-  
  
 *boundparam*  
 Indica el uso de parámetros adicionales. *boundparam* es un parámetro opcional que se debe especificar si el *scrollopt* valor PARAMETERIZED_STMT está establecida en ON.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 Si no se produce ningún error, sp_cursoropen devuelve uno de los siguientes valores.  
  
 0  
 El procedimiento que se ha ejecutado correctamente.  
  
 0x0001  
 Se produjo un error durante la ejecución (un error secundario, no lo suficientemente grave como para generar un error en la operación).  
  
 0x0002  
 Está en curso una operación asincrónica.  
  
 0x0002  
 Está en curso una operación FETCH.  
  
 A  
 Este cursor se ha desasignado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y no está disponible.  
  
 Cuando se produce un error, los valores devueltos pueden ser incoherentes y no se puede garantizar la exactitud.  
  
 Cuando el *rowcount* parámetro se especifica como un valor devuelto, se produce el siguiente conjunto de resultados.  
  
 -1  
 Se devuelve si el número de filas es desconocido o no es aplicable.  
  
 -n  
 Se devuelve cuando está en vigor un rellenado asincrónico. Representa el número de filas que se colocaron en la captura del búfer cuando el *scrollopt* valor AUTO_FETCH.  
  
 Si se usa una RPC, los valores devueltos son los siguientes.  
  
 0  
 El procedimiento es correcto.  
  
 1  
 Se produjo un error en el procedimiento.  
  
 2  
 Se genera un cursor de conjunto de claves de forma asincrónica.  
  
 16  
 Se ha cerrado automáticamente un cursor de avance rápido.  
  
> [!NOTE]  
>  Si el procedimiento sp_cursoropen se ejecuta correctamente, la RPC devuelve los parámetros y se envía un conjunto de resultados con información de formato de columna de TDS (mensajes 0xa0 y 0xa1). Si no puede ejecutarse se envían uno o varios mensajes de error TDS. En cualquier caso, no se devolverá ningún dato de fila y la *realiza* recuento de mensajes será cero. Si usa una versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anterior a la 7.0, se devuelven 0xa0, 0xa1 (estándar de las instrucciones SELECT) junto con las flujos de token 0xa5 y 0xa4. Si usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0, se devuelve 0x81 (estándar para las instrucciones SELECT) junto con las flujos de token 0xa5 y 0xa4.  
  
## <a name="remarks"></a>Notas  
  
## <a name="stmt-parameter"></a>Parámetro stmt  
 Si *stmt* especifica la ejecución de un procedimiento almacenado, los parámetros de entrada bien pueden definirse como constantes como parte de la *stmt* de cadena, o si especifica como *boundparam* argumentos. Las variables declaradas se pueden pasar como parámetros enlazados de esta manera.  
  
 El contenido permitido del *stmt* parámetro dependen de si o no la *ccopt* devuelto ALLOW_DIRECT por o para el resto del valor que se ha vinculado el *ccopt* valores, es decir:  
  
-   Si no se especifica ALLOW_DIRECT, ya sea un [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT o EXECUTE llamar a una instrucción para que se debe usar un procedimiento almacenado que contiene una única instrucción SELECT. Además, la instrucción SELECT debe calificarse como un cursor; es decir, no puede contener las palabras clave SELECT INTO o FOR BROWSE.  
  
-   Si se especifica ALLOW_DIRECT, esto puede dar como resultado una o más instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)], incluso aquellas que, a su vez, ejecuten otros procedimientos almacenados con varias instrucciones. Las instrucciones que no sean SELECT o cualquier instrucción SELECT que contenga las palabras clave SELECT INTO o FOR BROWSE simplemente se ejecutarán y no darán como resultado la creación de un cursor. Lo mismo puede decirse de cualquier instrucción SELECT incluida en un lote de varias instrucciones. En los casos en los que una instrucción SELECT contenga cláusulas que solo sean relativas a los cursores, dichas cláusulas se omiten. Por ejemplo, cuando el valor de *ccopt* es 0 x 2002, se trata de una solicitud para:  
  
    -   Un cursor con bloqueos de desplazamiento, si solo hay una instrucción SELECT que se califica como un cursor, o  
  
    -   La ejecución de una instrucción directa si hay varias instrucciones, una sola instrucción distinta de SELECT o una instrucción SELECT que no se califica como un cursor.  
  
## <a name="scrollopt-parameter"></a>Parámetro scrollopt  
 Los cinco primeros *scrollopt* valores (KEYSEY, DYNAMIC, FORWARD_ONLY, STATIC y FAST_FORWARD) son mutuamente excluyentes.  
  
 PARAMETERIZED_STMT y CHECK_ACCEPTED_TYPES se pueden vincular mediante OR a cualquiera de los primeros cinco valores.  
  
 AUTO_FETCH y AUTO_CLOSE se pueden vincular mediante OR a FAST_FORWARD.  
  
 Si CHECK_ACCEPTED_TYPES es ON, al menos uno de los últimos cinco *scrollopt* valores (KEYSET_ACCEPTABLE`,` DYNAMIC_ACCEPTABLE, FORWARD_ONLY_ACCEPTABLE, STATIC_ACCEPTABLE o FAST_FORWARD_ACCEPTABLE) también debe ser ON.  
  
 Los cursores STATIC se abren siempre como READ_ONLY. Esto significa que la tabla subyacente no se puede actualizar a través de este cursor.  
  
## <a name="ccopt-parameter"></a>Parámetro ccopt  
 Los primeros cuatro *ccopt* valores (READ_ONLY, SCROLL_LOCKS y ambos valores OPTIMISTIC) son mutuamente excluyentes.  
  
> [!NOTE]  
>  Elegir una de las cuatro primeras *ccopt* valores determina si el cursor es de solo lectura, o si se usan métodos optimistas o de bloqueos para evitar la pérdida de actualizaciones. Si un *ccopt* valor no se especifica, el valor predeterminado es OPTIMISTIC.  
  
 ALLOW_DIRECT y CHECK_ACCEPTED_TYPES se pueden vincular mediante OR a cualquiera de los primeros cuatro valores.  
  
 UPDT_IN_PLACE se puede vincular mediante OR a READ_ONLY, SCROLL_LOCKS o a cualquiera de los valores OPTIMISTIC.  
  
 Si CHECK_ACCEPTED_TYPES es ON, al menos uno de los últimos cuatro *ccopt* valores (READ_ONLY_ACCEPTABLE, SCROLL_LOCKS_ACCEPTABLE y cualquiera de los valores OPTIMISTIC_ACCEPTABLE) también deben ser ON.  
  
 Funciones UPDATE y DELETE posicionadas pueden realizarse únicamente en el búfer de captura y solo si el *ccopt* valor es igual a SCROLL_LOCKS u OPTIMISTIC. Si SCROLL_LOCKS es el valor especificado, se garantiza que la operación se realiza correctamente. Si el valor especificado es OPTIMISTIC, se producirá un error en la operación si la fila ha cambiado desde que se capturó en último lugar.  
  
 La razón de este error es que cuando el valor especificado es OPTIMISTIC, una función de control de simultaneidad optimista se realiza comparando las marcas de tiempo o los valores de las sumas de comprobación, según determina [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si alguna de estas filas no coincide, se producirá un error en la operación.  
  
 Especificar UPDT_IN_PLACE como valor devuelto produce los siguientes resultados:  
  
-   Si no está establecido al realizar una actualización colocada en una tabla con un único índice, el cursor elimina la fila de su tabla de trabajo y la inserta al final de alguna de las columnas de clave que usa el cursor, con lo que las cambia.  
  
-   Si está establecida en ON, el cursor simplemente actualizará las columnas de clave en la fila original de la tabla de trabajo.  
  
## <a name="boundparam-parameter"></a>Parámetro bound_param  
 El nombre del parámetro debe ser *paramdef* cuando se especifica PARAMETERIZED_STMT, según el mensaje de error en el código. Cuando no se especifica PARAMETERIZED_STMT, no se especifica ningún nombre en el mensaje de error.  
  
## <a name="rpc-considerations"></a>Consideraciones sobre RPC  
 La marca de entrada RPC RETURN_METADATA puede establecerse en 0x0001 para solicitar que se devuelvan los metadatos de la lista de selección del cursor en el flujo de TDS.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="boundparam-parameter"></a>Parámetro bound_param  
 Cualquier parámetro después del quinto se pasa como parámetro de entrada al plan de instrucción. El primer parámetro debe ser una cadena con el formato:  
  
 *{nombre de variable local de tipo de datos} [,... n].*  
  
 Los parámetros siguientes se utilizan para pasar los valores que se sustituirá para los *nombre de variable local* en la instrucción.  
  
## <a name="see-also"></a>Vea también  
 [sp_cursorfetch &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
