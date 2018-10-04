---
title: Aplicar un filtro a un modelo de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- model filter [data mining]
- filters [data mining]
- filtering input rows [Analysis Services]
- filtering data [Analysis Services]
ms.assetid: 4d0abeb5-e939-46d3-9097-6e0358244300
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4b851f631535008d1655a35c4b4af5321c8c4534
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48159995"
---
# <a name="apply-a-filter-to-a-mining-model"></a>Aplicar un filtro a un modelo de minería de datos
  Si la estructura de minería de datos contiene una tabla anidada, puede aplicar un filtro a la tabla de casos, a la tabla anidada o a ambas.  
  
 El siguiente procedimiento muestra cómo crear ambos tipos de filtros: filtros de casos y filtros de filas de tabla anidada.  
  
 La condición de la tabla de casos limita los clientes a aquéllos con ingresos entre 30000 y 40000. La condición de la tabla anidada limita los clientes a aquéllos que no compraron un producto determinado.  
  
 La condición de filtro completa creada en este ejemplo es la siguiente:  
  
```  
[Income] > '30000'   
AND  [Income] < '40000'   
AND EXISTS (SELECT * FROM [<nested table name>]   
WHERE [Model] <> 'Water Bottle' )   
```  
  
### <a name="to-create-a-case-filter-on-a-mining-model"></a>Para crear un filtro de casos en un modelo de minería de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], en el Explorador de soluciones, haga clic en la estructura de minería de datos que contiene el modelo de minería que desea filtrar.  
  
2.  Haga clic en la pestaña **Modelos de minería de datos** .  
  
3.  Seleccione el modelo y haga clic con el botón secundario del mouse para abrir el menú contextual.  
  
     O bien  
  
     Seleccione el modelo. A continuación, en el menú **Modelo de minería de datos** , seleccione **Establecer filtro de modelos**.  
  
4.  En el cuadro de diálogo **Filtro del modelo** , haga clic en la fila superior de la cuadrícula en el cuadro de texto **Columna de la estructura de minería de datos** .  
  
5.  Si el origen de datos contiene una única tabla plana, la lista desplegable mostrará únicamente los nombres de las columnas de dicha tabla.  
  
     Si la estructura de minería de datos contiene varias tablas, la lista mostrará los nombres de las tablas de origen. Los nombres de columna no se muestran hasta que se seleccione una tabla.  
  
     Si la estructura de minería de datos contiene una tabla de casos y una tabla anidada, la lista desplegable mostrará las columnas de la tabla de casos y el nombre de la tabla anidada.  
  
6.  Seleccione una columna en la lista desplegable.  
  
     El icono en la parte izquierda del cuadro de texto cambia para indicar que el elemento seleccionado es una tabla o una columna.  
  
7.  Haga clic en el cuadro de texto **Operador** y seleccione un operador de la lista. Los operadores válidos cambian en función del tipo de datos de la columna seleccionada.  
  
8.  Haga clic en el cuadro de texto **Valor** y escriba un valor:  
  
     Por ejemplo, seleccione `Income` como columna, seleccione el mayor que (>) de operador y, a continuación, escriba `30000`.  
  
9. Haga clic en la siguiente fila de la cuadrícula.  
  
     La condición de filtro creada se agrega automáticamente al cuadro de texto Expresión. Por ejemplo, `[Income] > '30000'`  
  
10. Haga clic en el cuadro de texto **Y/O** de la siguiente fila de la cuadrícula para agregar una condición.  
  
     Por ejemplo, para crear una condición BETWEEN, seleccione `AND` en la lista desplegable de operandos lógicos.  
  
11. Seleccione un operador y escriba un valor tal como se describe en los pasos 7 y 8.  
  
     Por ejemplo, seleccione `Income` como la columna de nuevo, seleccione el operador menor que (<) y, a continuación, escriba `40000`.  
  
12. Haga clic en la siguiente fila de la cuadrícula.  
  
13. La condición  de filtro en el cuadro de texto Expresión se actualiza automáticamente para incluir la nueva condición. La expresión completa es la siguiente: `[Income] > '30000'AND [Income] < '40000'`  
  
### <a name="to-add-a-filter-on-the-nested-table-in-a-mining-model"></a>Para agregar un filtro en la tabla anidada en un modelo de minería de datos  
  
1.  En el  **\<nombre > filtro del modelo** diálogo cuadro, haga clic en una fila vacía en la cuadrícula situada debajo **columna de estructura de minería de datos**.  
  
2.  Seleccione el nombre de la tabla anidada en la lista desplegable.  
  
     El icono en la parte izquierda del cuadro de texto cambiará para indicar que el elemento seleccionado es el nombre de una tabla.  
  
3.  Haga clic en el cuadro de texto **Operador** y seleccione **Contiene** o **No contiene**.  
  
     Éstas son las únicas condiciones disponibles para la tabla anidada en el cuadro de diálogo **Filtro de modelos** , porque se está restringiendo la tabla de casos a únicamente los casos que contienen un cierto valor en la tabla anidada. En el paso siguiente, se establecerá el valor de la condición en la tabla anidada.  
  
4.  Haga clic en el cuadro **Valor** y, después, seleccione el botón **(…)** para crear una expresión.  
  
     El  **\<nombre > filtro** abre el cuadro de diálogo. Este cuadro de diálogo solo puede establecer condiciones en la tabla actual, que en este caso es la tabla anidada.  
  
5.  Haga clic en el cuadro **Columna de la estructura de minería de datos** y seleccione un nombre de columna en las listas desplegables de las columnas de tabla anidadas.  
  
6.  Haga clic en **Operador** y seleccione un operador en la lista de operadores válidos para la columna.  
  
7.  Haga clic en **Valor** y escriba un valor.  
  
     Por ejemplo, para **columna de estructura de minería de datos,** seleccione `Model`. Para **operador**, seleccione `<>`y escriba el valor `Water Bottle`. Esta condición crea la siguiente expresión de filtro:  
  
```  
EXISTS (SELECT * FROM [<nested table name>] WHERE [Model] <> 'Water Bottle' )   
```  
  
> [!NOTE]  
>  Dado que el número de atributos de tabla anidada es potencialmente ilimitado, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no suministra ninguna lista de valores posibles entre los que seleccionar. Debe escribir el valor exacto. Asimismo, no se puede utilizar a un operador LIKE en una tabla anidada.  
  
1.  Agregue más condiciones según convenga y combínelas seleccionando `AND` o `OR` en el **o** cuadro en el lado izquierdo de la **condiciones** cuadrícula. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
2.  En el cuadro de diálogo **Filtro del modelo** , revise las condiciones que creó utilizando el cuadro de diálogo **Filtro** . Las condiciones de la tabla anidada se anexan a las condiciones de la tabla de casos y el conjunto completo de condiciones de filtro se muestra en el cuadro de texto **Expresión** .  
  
3.  Si lo desea, haga clic en **Editar consulta** para cambiar manualmente la expresión de filtro.  
  
    > [!NOTE]  
    >  Si cambia manualmente una parte de la expresión de filtro, la cuadrícula se deshabilitará y a partir de este momento deberá trabajar solo con la expresión de filtro en modo de edición de texto. Para restaurar el modo de edición de cuadrícula, debe borrar la expresión de filtro y comenzar de nuevo.  
  
  
## <a name="see-also"></a>Vea también  
 [Filtros para modelos de minería de datos de &#40;Analysis Services - minería de datos&#41;](mining-models-analysis-services-data-mining.md)   
 [Tareas del modelo de minería de datos y procedimientos](mining-model-tasks-and-how-tos.md)   
 [Eliminar un filtro de un modelo de minería de datos](delete-a-filter-from-a-mining-model.md)  
  
  
