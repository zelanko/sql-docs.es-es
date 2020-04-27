---
title: Cómo representa combinaciones el diseñador de consultas y vistas (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL pane [Visual Database Tools]
- joins [SQL Server], Query and View Designer
- Diagram pane [Visual Database Tools]
ms.assetid: 20a99dcb-83bd-4aa6-9139-92e2e5ba4887
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: abd8dd7c3c23a13b1cdff7a2d6f76fb99375a641
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63155266"
---
# <a name="how-the-query-and-view-designer-represents-joins-visual-database-tools"></a>Cómo representa combinaciones el Diseñador de consultas y vistas (Visual Database Tools)
  Si las tablas están combinadas, el [Diseñador de consultas y vistas](visual-database-tools.md) representa la combinación de forma gráfica en el [panel Diagrama](diagram-pane-visual-database-tools.md) y mediante sintaxis SQL en el [panel SQL](sql-pane-visual-database-tools.md).  
  
## <a name="diagram-pane"></a>panel Diagrama  
 En el panel Diagrama, el Diseñador de consultas y vistas muestra una línea de combinación entre las columnas de datos implicadas en la combinación. El Diseñador de consultas y vistas muestra una línea de combinación para cada condición de combinación. Por ejemplo, la ilustración siguiente muestra una línea de combinación entre dos tablas que están combinadas:  
  
 ![La línea de combinación muestra la relación entre dos tablas](../../database-engine/media//dv3wbig.gif "La línea de combinación muestra la relación entre dos tablas")  
  
 Si las tablas están combinadas mediante más de una condición de combinación, el Diseñador de consultas y vistas muestra varias líneas de combinación, como en el ejemplo siguiente:  
  
 ![Tablas combinadas usando más de una condición de combinación](../../database-engine/media//dv3w9n1.gif "Tablas combinadas usando más de una condición de combinación")  
  
 Si no se muestran las columnas de datos combinadas (por ejemplo, el rectángulo que representa la tabla o el objeto con estructura de tabla está minimizado o la combinación incluye una expresión), el Diseñador de consultas coloca la línea de combinación en la barra de título del rectángulo que representa la tabla o el objeto con estructura de tabla.  
  
 La forma del icono situado en el centro de la línea de combinación indica cómo se combinan las tablas u objetos con estructura de tabla. Si la cláusula de combinación utiliza un operador que no sea igual (=), el operador se muestra en el icono de línea de combinación. La tabla siguiente muestra los iconos que aparecen en la línea de combinación.  
  
|**Icono de línea de combinación**|**Descripción**|  
|------------------------|---------------------|  
|![Icono de Visual Database Tools](../../database-engine/media//dv3wbih.gif "Icono de Visual Database Tools")|Combinación interna (creada mediante un signo igual).|  
|![Icono de Visual Database Tools](../../database-engine/media//dv3wbii.gif "Icono de Visual Database Tools")|Combinación interna basada en el operador "mayor que".|  
|![Icono de Visual Database Tools](../../database-engine/media//dv3wbij.gif "Icono de Visual Database Tools")|Combinación externa en la que se incluirán todas las filas de la tabla representada a la izquierda, incluso si no tienen coincidencias en la tabla relacionada.|  
|![Icono de Visual Database Tools](../../database-engine/media//dv3wbik.gif "Icono de Visual Database Tools")|Combinación externa en la que se incluirán todas las filas de la tabla representada a la derecha, incluso si no tienen coincidencias en la tabla relacionada.|  
|![Icono de Visual Database Tools](../../database-engine/media//dv3wbil.gif "Icono de Visual Database Tools")|Combinación externa completa en la que se incluirán todas las filas de ambas tablas, incluso si no tienen coincidencias en la tabla relacionada.|  
  
 Los símbolos situados en los extremos de la línea de combinación indican el tipo de combinación. La tabla siguiente muestra los tipos de combinaciones y los iconos que aparecen en los extremos de la línea de combinación.  
  
|**Icono situado en los extremos de la línea de combinación**|**Tipo de combinación**|  
|-----------------------------------|----------------------|  
|![Icono de Visual Database Tools](../../database-engine/media//dv3wbim.gif "Icono de Visual Database Tools")|Combinación uno a uno.|  
|![Icono de Visual Database Tools](../../database-engine/media//dv3wbin.gif "Icono de Visual Database Tools")|Combinación uno a varios.|  
|![Icono de Visual Database Tools](../../database-engine/media//dv3wbio.gif "Icono de Visual Database Tools")|El Diseñador de consultas y vistas no puede determinar el tipo de combinación. Esta situación ocurre con más frecuencia cuando ha creado una combinación de forma manual.|  
  
## <a name="sql-pane"></a>panel SQL  
 Una combinación puede expresarse de varias maneras en una instrucción SQL. La sintaxis exacta depende de la base de datos que esté utilizando y de la forma en que haya definido la combinación.  
  
 Las opciones de sintaxis para combinar tablas incluyen:  
  
-   **Calificador JOIN para la cláusula FROM**.   Las palabras clave INNER y OUTER especifican el tipo de combinación. Esta sintaxis es estándar para SQL ANSI 92.  
  
     Por ejemplo, si combina las tablas `publishers` y `pub_info` según la columna `pub_id` de cada tabla, la instrucción SQL resultante podría tener el siguiente aspecto:  
  
    ```  
    SELECT *  
    FROM publishers INNER JOIN pub_info ON  
       publishers.pub_id = pub_info.pub_id  
    ```  
  
     Si crea una combinación externa, aparecen las palabras LEFT OUTER o RIGHT OUTER en lugar de la palabra INNER.  
  
-   **La cláusula WHERE compara columnas de ambas tablas**.   Aparecerá una cláusula WHERE si la base de datos no admite la sintaxis JOIN, o si la especificó el usuario. Si la combinación se crea en la cláusula WHERE, ambos nombres de tabla aparecen en la cláusula FROM.  
  
     Por ejemplo, la instrucción siguiente combina las tablas `publishers` y `pub_info` .  
  
    ```  
    SELECT *  
    FROM publishers, pub_info  
    WHERE publishers.pub_id = pub_info.pub_id  
    ```  
  
## <a name="see-also"></a>Consulte también  
 [Realizar consultas con combinaciones &#40;Visual Database Tools&#41;](query-with-joins-visual-database-tools.md)   
 [Cuadro de diálogo Combinar &#40;Visual Database Tools&#41;](join-dialog-box-visual-database-tools.md)  
  
  
