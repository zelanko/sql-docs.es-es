---
title: 'Apéndice B: Tablas de transición de estado ODBC Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- state transitions [ODBC]
- transitioning states [ODBC], about state transitions
- state transitions [ODBC], about state transitions
ms.assetid: 15088dbe-896f-4296-b397-02bb3d0ac0fb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: db20c492ababbe6bf8f065fce88067c643f2694d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302889"
---
# <a name="appendix-b-odbc-state-transition-tables"></a>Apéndice B: Tablas de transición de estado de ODBC
Las tablas de este apéndice muestran cómo las funciones ODBC causan transiciones del entorno, la conexión, la instrucción y los estados del descriptor. El estado del entorno, la conexión, la instrucción o el descriptor normalmente dicta cuándo se puede llamar a las funciones que utilizan el tipo correspondiente de identificador (entorno, conexión, instrucción o descriptor). Los estados de entorno, conexión, instrucción y descriptor se superponen aproximadamente como se muestra en las siguientes ilustraciones. Por ejemplo, la superposición exacta de los estados de conexión C5 y C6 y los estados de instrucción S1 a S12 depende del origen de datos, ya que las transacciones comienzan en momentos diferentes en orígenes de datos diferentes, y el estado del descriptor D1i (descriptor asignado implícitamente) depende del estado de la instrucción con la que está asociado el descriptor, mientras que el estado D1e (descriptor asignado explícitamente) es independiente del estado de cualquier instrucción. Para obtener una descripción de cada estado, vea [Transiciones](../../../odbc/reference/appendixes/environment-transitions.md)de entorno , [Transiciones](../../../odbc/reference/appendixes/connection-transitions.md)de conexión , Transiciones de [instrucción](../../../odbc/reference/appendixes/statement-transitions.md)y [Transiciones](../../../odbc/reference/appendixes/descriptor-transitions.md)de descriptor , más adelante en este apéndice.  
  
 Los estados de entorno y conexión se superponen de la siguiente manera:  
  
 ![Los estados del entorno y de la conexión se superponen](../../../odbc/reference/appendixes/media/app01.gif "app01")  
  
 Los estados de conexión e instrucción se superponen de la siguiente manera:  
  
 ![Los estados de la conexión y la instrucción se superponen](../../../odbc/reference/appendixes/media/app02.gif "app02")  
  
 Los estados de instrucción y descriptor se superponen de la siguiente manera:  
  
 ![Los estados de la instrucción y del descriptor se superponen](../../../odbc/reference/appendixes/media/app03.gif "app03")  
  
 Los estados de conexión y descriptor se superponen de la siguiente manera:  
  
 ![Los estados de la conexión y del descriptor se superponen](../../../odbc/reference/appendixes/media/app04.gif "app04")  
  
 Cada entrada de una tabla de transición puede ser uno de los siguientes valores:  
  
-   **--**-El estado no cambia después de ejecutar la función.  
  
-   **E**  

     **_n_** , **C_n_**, **S_n_** o **D_n_:** el estado del entorno, la conexión, la instrucción o el descriptor se mueve al estado especificado.  
 
-   **(IH):** se pasó un identificador no válido a la función. Si el identificador era un identificador nulo o era un identificador válido del tipo incorrecto (por ejemplo, se pasó un identificador de conexión cuando se requería un identificador de instrucción), la función devuelve SQL_INVALID_HANDLE; de lo contrario el comportamiento es indefinido y probablemente fatal. Este error solo se muestra cuando es el único resultado posible de llamar a la función en el estado especificado. Este error no cambia el estado y siempre es detectado por el Administrador de controladores, como se indica en los paréntesis.  
  
-   **NS** - Próximo estado. La transición de la instrucción es la misma que si la instrucción no hubiera pasado por los estados asincrónicos. Por ejemplo, supongamos que una instrucción que crea un conjunto de resultados entra en el estado S11 desde el estado S1 porque **SQLExecDirect** devolvió SQL_STILL_EXECUTING. La notación NS en el estado S11 significa que las transiciones para la instrucción son las mismas que las de una instrucción en el estado S1 que crea un conjunto de resultados. Si **SQLExecDirect** devuelve un error, la instrucción permanece en el estado S1; si se realiza correctamente, la instrucción se mueve al estado S5; si necesita datos, la instrucción se mueve al estado S8; y si sigue ejecutándose, permanece en el estado S11.  

-   **_XXXXX_** o **(*XXXXX*)** - Un SQLSTATE que está relacionado con la tabla de transición; SQLSTATEs detectados por el Administrador de controladores se incluyen entre paréntesis. La función devuelta SQL_ERROR y el SQLSTATE especificado, pero el estado no cambia. Por ejemplo, si **sqlExecute** se llama antes de **SQLPrepare**, devuelve SQLSTATE HY010 (error de secuencia de funciones).  

> [!NOTE]  
>  Las tablas no muestran errores no relacionados con las tablas de transición que no cambian el estado. Por ejemplo, cuando **sqlAllocHandle** se llama en el estado de entorno E1 y devuelve SQLSTATE HY001 (error de asignación de memoria), el entorno permanece en el estado E1; esto no se muestra en la tabla de transición de entorno para **SQLAllocHandle**.  
  
 Si el entorno, la conexión, la instrucción o el descriptor pueden moverse a más de un estado, se muestra cada estado posible y una o varias notas al pie explican las condiciones en las que tiene lugar cada transición. Las siguientes notas al pie pueden aparecer en cualquier tabla.  
  
|Nota|Significado|  
|--------------|-------------|  
|b|Antes o después. El cursor se colocó antes del inicio del conjunto de resultados o después del final del conjunto de resultados.|  
|c|Función actual. La función actual se ejecutaba de forma asincrónica.|  
|d|Necesita datos. La función devolvió SQL_NEED_DATA.|  
|e|Error. La función devolvió SQL_ERROR.|  
|i|Fila no válida. El cursor se colocó en una fila del conjunto de resultados y la fila se había eliminado o se había producido un error en una operación de la fila. Si existía la matriz de estado de fila, el valor de la matriz de estado de fila de la fila era SQL_ROW_DELETED o SQL_ROW_ERROR. (La matriz de estado de fila es señalada por el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR.)|  
|nf|Not found. La función devolvió SQL_NO_DATA. Esto no se aplica cuando **SQLExecDirect**, **SQLExecute**o **SQLParamData** devuelve SQL_NO_DATA después de ejecutar una instrucción de actualización o eliminación buscada.|  
|np|No preparado. La declaración no estaba preparada.|  
|nr|Especifica que no hay resultados. La instrucción no creará o no un conjunto de resultados.|  
|o|Otra función. Otra función se ejecutaba de forma asincrónica.|  
|p|Preparado. La declaración fue preparada.|  
|r|Resultados. La instrucción creará o sí un conjunto de resultados (posiblemente vacío).|  
|s|Correcto. La función devuelve SQL_SUCCESS_WITH_INFO o SQL_SUCCESS.|  
|v|Fila válida. El cursor se colocó en una fila del conjunto de resultados y la fila se ha insertado correctamente, se ha actualizado correctamente u otra operación de la fila se ha completado correctamente. Si la matriz de estado de fila existía, el valor de la matriz de estado de fila de la fila era SQL_ROW_ADDED, SQL_ROW_SUCCESS o SQL_ROW_UPDATED. (La matriz de estado de fila es señalada por el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR.)|  
|x|En ejecución. La función devuelve SQL_STILL_EXECUTING.|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 En este ejemplo, la fila de la tabla de transición de estado de entorno para **SQLFreeHandle** cuando *HandleType* es SQL_HANDLE_ENV es la siguiente.  
  
|E0<br /><br /> Sin asignar|E1<br /><br /> Allocated|E2<br /><br /> Conexión|  
|------------------------|----------------------|-----------------------|  
|(IH)|E0|(HY010)|  
  
 Si **SQLFreeHandle** se llama en el estado de entorno E0 con *HandleType* establecido en SQL_HANDLE_ENV, el Administrador de controladores devuelve SQL_INVALID_HANDLE. Si se llama en el estado E1 con *HandleType* establecido en SQL_HANDLE_ENV, el entorno se mueve al estado E0 si la función se realiza correctamente y permanece en el estado E1 si se produce un error en la función. Si se llama en el estado E2 con *HandleType* establecido en SQL_HANDLE_ENV, el Administrador de controladores siempre devuelve SQL_ERROR y SQLSTATE HY010 (error de secuencia de funciones) y el entorno permanece en el estado E2.  
  
 Para comprender las tablas de transición de estado, es necesario comprender a qué elemento (entorno, conexión, instrucción o descriptor) hacen referencia. Supongamos que una función acepta el identificador de un elemento de tipo X. La tabla de transición de estado X para esa función describe cómo la llamada a la función, con el identificador de un elemento de tipo X, afecta a ese elemento. Por ejemplo, **SQLDisconnect** acepta un identificador de conexión. La tabla de transición de estado de conexión para **SQLDisconnect** describe cómo **SQLDisconnect** afecta al estado de la conexión para la que se llama.  
  
 Supongamos que una función acepta el identificador de un elemento de tipo Y, donde Y no es igual a X. La tabla de transición de estado X para esa función describe cómo la llamada a la función, con un identificador de tipo X asociado al elemento de tipo Y, afecta al elemento de tipo Y. Por ejemplo, la tabla de transición de estado de instrucción para **SQLDisconnect** describe cómo **SQLDisconnect** afecta al estado de una instrucción cuando se llama con el identificador de la conexión con la que está asociada la instrucción.  
  
 Este apéndice contiene los siguientes temas.  
  
-   [Transiciones de entorno](../../../odbc/reference/appendixes/environment-transitions.md)  
  
-   [Transiciones de conexión](../../../odbc/reference/appendixes/connection-transitions.md)  
  
-   [Transiciones de instrucción](../../../odbc/reference/appendixes/statement-transitions.md)  
  
-   [Transiciones de descriptor](../../../odbc/reference/appendixes/descriptor-transitions.md)
