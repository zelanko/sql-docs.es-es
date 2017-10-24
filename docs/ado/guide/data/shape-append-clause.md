---
title: "Forma cláusula APPEND | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], APPEND clause
- append clause [ADO]
ms.assetid: f90fcf55-6b24-401d-94e1-d65bd24bd342
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 52c9495e221ba7a4b71ba91d276eefd576f6715d
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="shape-append-clause"></a>Cláusula APPEND Shape
La cláusula APPEND del comando shape anexa una o varias columnas para un **conjunto de registros**. Con frecuencia, estas columnas son columnas de capítulo, que hacen referencia a un elemento secundario **conjunto de registros**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SHAPE [parent-command [[AS] parent-alias]] APPEND column-list  
```  
  
## <a name="description"></a>Description  
 Los elementos de esta cláusula son los siguientes:  
  
 *comando primario*  
 Cero o uno de los siguientes valores (se puede omitir el *comando primario* completamente):  
  
-   Un comando de proveedor entre llaves ("{}") que devuelve un **Recordset** objeto. El comando se emite al proveedor de datos subyacente, y su sintaxis depende de los requisitos de ese proveedor. Normalmente será el lenguaje SQL, si bien ADO no requiere ningún lenguaje de consulta determinado.  
  
-   Otro comando shape incrustado entre paréntesis.  
  
-   La tabla (palabra clave), seguido del nombre de una tabla en el proveedor de datos.  
  
 *alias del primario*  
 Un alias opcional que hace referencia al elemento primario **conjunto de registros**.  
  
 *lista de columnas*  
 Uno o varios de los siguientes valores:  
  
-   Una columna agregada.  
  
-   Una columna calculada.  
  
-   Una nueva columna creada mediante la cláusula nuevo.  
  
-   Una columna de capítulo. Una definición de columna de capítulo se encierra entre paréntesis ("()"). Vea la siguiente sintaxis.  
  
```  
SHAPE [parent-command [[AS] parent-alias]]  
   APPEND (child-recordset [ [[AS] child-alias]   
      RELATE parent-column TO child-column | PARAMETER param-number, ... ])  
   [[AS] chapter-alias]   
   [, ... ]  
```  
  
## <a name="remarks"></a>Comentarios  
 *conjunto de registros secundario*  
 -   Un comando de proveedor entre llaves ("{}") que devuelve un **Recordset** objeto. El comando se emite al proveedor de datos subyacente, y su sintaxis depende de los requisitos de ese proveedor. Normalmente será el lenguaje SQL, si bien ADO no requiere ningún lenguaje de consulta determinado.  
  
-   Otro comando shape incrustado entre paréntesis.  
  
-   El nombre de un objeto en forma de **conjunto de registros**.  
  
-   La tabla (palabra clave), seguido del nombre de una tabla en el proveedor de datos.  
  
 *alias de elemento secundario*  
 Un alias que hace referencia al formulario secundario **conjunto de registros**.  
  
 *columna primaria*  
 Una columna en la **Recordset** devuelto por la *comando primario.*  
  
 *columna secundaria*  
 Una columna en la **Recordset** devuelto por la *comando secundario*.  
  
 *número de parámetros*  
 Vea [el funcionamiento de los comandos parametrizados](../../../ado/guide/data/operation-of-parameterized-commands.md).  
  
 *alias de capítulo*  
 Un alias que hace referencia a la columna de capítulo anexada al elemento primario.  
  
> [!NOTE]
>  El *"columna primaria* TO *columna secundaria"* cláusula es en realidad una lista, donde cada relación definida se separa por comas  
  
> [!NOTE]
>  La cláusula después de la palabra clave APPEND es en realidad una lista, donde cada cláusula separado por una coma y define otra columna que se debe anexar al elemento primario.  
  
## <a name="remarks"></a>Comentarios  
 Al crear comandos de proveedor de proporcionados por el usuario como parte de un comando SHAPE, forma tratará proporcionada por el usuario un comando de proveedor como una cadena opaca y pasará fielmente al proveedor. Por ejemplo, en el siguiente comando SHAPE,  
  
```  
SHAPE {select * from t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 SHAPE ejecutará dos comandos: `select * from t1` y (`select * from t2 RELATE k1 TO k2)`. Si el usuario proporciona un comando compuesto que consta de varios comandos de proveedor separados por punto y coma, SHAPE no es capaz de distinguir la diferencia. Por lo que en el siguiente comando SHAPE,  
  
```  
SHAPE {select * from t1; drop table t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 Ejecuta de forma `select * from t1; drop table t1` y (`select * from t2 RELATE k1 TO k2),` sin darse cuenta que `drop table t1` es un independiente y en este comando de proveedor de caso, peligroso. Las aplicaciones siempre deben validar la entrada del usuario para impedir que estos posibles ataques de piratas informáticos que se producen.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Funcionamiento de los comandos sin parámetros](../../../ado/guide/data/operation-of-non-parameterized-commands.md)  
  
-   [Funcionamiento de los comandos con parámetros](../../../ado/guide/data/operation-of-parameterized-commands.md)  
  
-   [Comandos híbridos](../../../ado/guide/data/hybrid-commands.md)  
  
-   [Cláusulas COMPUTE de forma que intervengan](../../../ado/guide/data/intervening-shape-compute-clauses.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la forma de datos](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática formal de forma](../../../ado/guide/data/formal-shape-grammar.md)   
 [Comandos Shape en General](../../../ado/guide/data/shape-commands-in-general.md)

