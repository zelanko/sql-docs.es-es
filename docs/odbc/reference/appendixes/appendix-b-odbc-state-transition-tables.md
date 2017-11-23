---
title: "Apéndice B: tablas de transición de estado de ODBC | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- state transitions [ODBC]
- transitioning states [ODBC], about state transitions
- state transitions [ODBC], about state transitions
ms.assetid: 15088dbe-896f-4296-b397-02bb3d0ac0fb
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2a191cb539aec61150f30d8c083dfba7dd2d2069
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="appendix-b-odbc-state-transition-tables"></a>Apéndice B: tablas de transición de estado de ODBC
Las tablas de este apéndice muestran cómo hacen que las transiciones del entorno, conexión, instrucción y Estados de descriptor funciones ODBC. Normalmente, el estado del entorno, conexión, instrucción o descriptor dicta cuando puede llamar a funciones que usan el tipo de identificador (entorno, conexión, instrucción o descriptor) correspondiente. Los Estados de entorno, conexión, instrucción y descriptor se superponen aproximadamente tal como se muestra en la siguiente ilustración. Por ejemplo, la superposición de conexión exacta Estados C5 y C6 y Estados de instrucción que s1 a través de S12 es, depende del origen de datos, ya que las transacciones empiezan en momentos diferentes en distintos orígenes de datos, y depende del estado de descriptor D1i (implícitamente asignado descriptor) en el estado de la instrucción que está asociado el descriptor, mientras que el estado D1e (asignado explícitamente descriptor) es independiente del estado de cualquier instrucción. Para obtener una descripción de cada estado, vea [transiciones de entorno](../../../odbc/reference/appendixes/environment-transitions.md), [conexión transiciones](../../../odbc/reference/appendixes/connection-transitions.md), [transiciones de instrucción](../../../odbc/reference/appendixes/statement-transitions.md), y [Descriptor transiciones ](../../../odbc/reference/appendixes/descriptor-transitions.md), más adelante en este apéndice.  
  
 Los Estados de entorno y la conexión se superponen como sigue:  
  
 ![Estados de entorno y la conexión se superponen](../../../odbc/reference/appendixes/media/app01.gif "app01")  
  
 Los Estados de conexión y la instrucción se superponen como sigue:  
  
 ![Conexión y la instrucción se superponen los estados](../../../odbc/reference/appendixes/media/app02.gif "app02")  
  
 Los Estados de instrucción y el descriptor se superponen como sigue:  
  
 ![Instrucción y del descriptor se superponen los estados](../../../odbc/reference/appendixes/media/app03.gif "app03")  
  
 Los Estados de conexión y del descriptor se superponen como sigue:  
  
 ![Conexión y del descriptor se superponen los estados](../../../odbc/reference/appendixes/media/app04.gif "app04")  
  
 Cada entrada de una tabla de transición puede ser uno de los siguientes valores:  
  
-   **--**No se modifica el estado después de ejecutar la función.  
  
-   **E**  
     ***n***,  **C*n***,  **S*n***, o  **D.*n***: el estado del entorno, conexión, instrucción o descriptor pasa al estado especificado.  
  
-   **(IH)**  : Se pasó un identificador no válido a la función. Si el identificador es un identificador nulo o es un identificador válido de un tipo incorrecto: por ejemplo, se pasó un identificador de conexión cuando se requiere un identificador de instrucción, la función devuelve SQL_INVALID_HANDLE; en caso contrario, el comportamiento es indefinido y probablemente irrecuperable. Este error se muestra solo cuando es el resultado solo es posible llamar a la función en el estado especificado. Este error no cambia el estado y siempre se detecta mediante el Administrador de controladores, como se indica en los paréntesis.  
  
-   **NS** : estado siguiente. La transición de instrucción es el mismo que si la instrucción no había pasado por los Estados asincrónicos. Por ejemplo, suponga que una instrucción que crea un conjunto de resultados entra en estado S11 de estado S1 porque **SQLExecDirect** devuelve SQL_STILL_EXECUTING. La notación de NS en estado S11 significa que las transiciones para la instrucción son los mismos que los de una instrucción en estado S1 que crea un conjunto de resultados. Si **SQLExecDirect** devuelve un error, la instrucción permanece en estado S1; si se realiza correctamente, la instrucción se mueve al estado S5; si necesita que los datos, la instrucción se mueve al estado S8; y si todavía se está ejecutando, permanece en estado S11.  
  
-   ***XXXXX*** o  **(*XXXXX*) **: un SQLSTATE, que está relacionado con la tabla de transición. SQLSTATE detectado por el Administrador de controladores se encierran entre paréntesis. La función devuelve SQL_ERROR y el valor de SQLSTATE especificado, pero no cambia el estado. Por ejemplo, si **SQLExecute** se llama antes de **SQLPrepare**, devuelve SQLSTATE HY010 (error de secuencia de función).  
  
> [!NOTE]  
>  Las tablas no muestran errores no relacionados con las tablas de transición que no cambian el estado. Por ejemplo, cuando **SQLAllocHandle** se invoca en el estado del entorno E1 y devuelve SQLSTATE HY001 (error de asignación de memoria), el entorno permanece en estado E1; esto no se muestra en la tabla de transiciones de entorno para  **SQLAllocHandle**.  
  
 Si el entorno, la conexión, la instrucción o el descriptor puede mover a más de un estado, se muestra cada posible estado y una o varias de las notas al pie explican las condiciones en las que realiza cada transición. Los pies de página siguientes pueden aparecer en cualquier tabla.  
  
|Nota al pie|Significado|  
|--------------|-------------|  
|b|Antes o después. El cursor se coloca antes del inicio del conjunto de resultados o después del final del conjunto de resultados.|  
|c|Función actual. La función actual se estaba ejecutando de forma asincrónica.|  
|d|Necesita los datos. La función devuelve SQL_NEED_DATA.|  
|e|Error. La función devuelve SQL_ERROR.|  
|i|Fila no válida. El cursor se coloca en una fila en el resultado se eliminó conjunto y la fila o se ha producido un error en una operación en la fila. Si existiera la matriz de Estados de fila, el valor de la matriz de estado de fila de la fila era SQL_ROW_DELETED o SQL_ROW_ERROR. (La matriz de Estados de fila está indicada por el atributo de instrucción de SQL_ATTR_ROW_STATUS_PTR.)|  
|NF|No se encuentra. La función devuelve SQL_NO_DATA. Esto no aplica cuando **SQLExecDirect**, **SQLExecute**, o **SQLParamData** devuelve SQL_NO_DATA después de ejecutar una búsqueda instrucción update o delete.|  
|np|No se ha preparado. No se ha preparado la instrucción.|  
|n|No hay resultados. La instrucción no puede o no ha creado un conjunto de resultados.|  
|o|Otra función. Otra función estaba ejecutando de forma asincrónica.|  
|p|Preparado. Se ha preparado la instrucción.|  
|r|Resultados. La instrucción se o ha creado un conjunto de resultados (posiblemente vacía).|  
|s|Correcto. La función devuelve SQL_SUCCESS_WITH_INFO o SQL_SUCCESS.|  
|v|Fila válida. El cursor se coloca en una fila del conjunto de resultados y la fila tenía ha insertado correctamente, se ha actualizado correctamente, o cualquier otra operación en la fila se hubiera realizado correctamente. Si existiera la matriz de Estados de fila, el valor de la matriz de estado de fila de la fila era SQL_ROW_ADDED, SQL_ROW_SUCCESS o SQL_ROW_UPDATED. (La matriz de Estados de fila está indicada por el atributo de instrucción de SQL_ATTR_ROW_STATUS_PTR.)|  
|x|En ejecución. La función devolvió SQL_STILL_EXECUTING.|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 En este ejemplo, la fila de la transición de estado del entorno de tabla para **SQLFreeHandle** cuando *HandleType* es SQL_HANDLE_ENV es como sigue.  
  
|E0<br /><br /> Sin asignar|E1<br /><br /> Asignado|E2<br /><br /> Conexión|  
|------------------------|----------------------|-----------------------|  
|(IH)|E0|(HY010)|  
  
 Si **SQLFreeHandle** se llama en el estado del entorno E0 con *HandleType* establecido en SQL_HANDLE_ENV, el Administrador de controladores devuelva SQL_INVALID_HANDLE. Si se llama en estado E1 con *HandleType* establecido en SQL_HANDLE_ENV, el entorno pasa a estado E0 si la función se realiza correctamente y permanece en estado E1 si se produce un error en la función. Si se llama en estado E2 con *HandleType* establecido en SQL_HANDLE_ENV, el Administrador de controladores siempre devuelve SQL_ERROR y SQLSTATE HY010 (error de secuencia de función) y el entorno permanece en estado E2.  
  
 Para entender las tablas de la transición de estado, es necesario comprender qué elemento (entorno, conexión, instrucción o descriptor) hacen referencia a. Supongamos que una función acepta el identificador de un elemento de tipo X. La tabla de transiciones de estado X para esa función describe cómo llamar a la función, con el identificador de un elemento de tipo X, afecta a ese elemento. Por ejemplo, **SQLDisconnect** acepta un identificador de conexión. La tabla de transiciones de estado de conexión para **SQLDisconnect** describe cómo **SQLDisconnect** afecta al estado de la conexión para el que se llama.  
  
 Supongamos que una función acepta el identificador de un elemento de tipo Y, en Y no es igual a X. La tabla de transiciones de estado X para esa función describe afecta a la llamada de la función, con un identificador de tipo X que está asociado con el elemento de tipo Y, el elemento de tipo Y. Por ejemplo, la instrucción transición tabla de estado para **SQLDisconnect** describe cómo **SQLDisconnect** afecta al estado de una instrucción cuando se llama con el identificador de la conexión con la que el instrucción está asociada.  
  
 Este apéndice contiene los temas siguientes.  
  
-   [Transiciones de entorno](../../../odbc/reference/appendixes/environment-transitions.md)  
  
-   [Transiciones de conexión](../../../odbc/reference/appendixes/connection-transitions.md)  
  
-   [Transiciones de instrucción](../../../odbc/reference/appendixes/statement-transitions.md)  
  
-   [Transiciones de descriptor](../../../odbc/reference/appendixes/descriptor-transitions.md)
