---
title: Crear consultas de actualización (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- tables [SQL Server], updating
- queries [SQL Server], types
- Update query
- updating tables
ms.assetid: 178b7b75-8078-4e61-b2a8-4719b9d8033d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 47951e101a5f8f480496c8570a22cd1a950b3309
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63270582"
---
# <a name="create-update-queries-visual-database-tools"></a>Crear consultas de actualización (Visual Database Tools)
  Puede cambiar el contenido de varias filas en una sola operación mediante una consulta Update. Por ejemplo, en una tabla `titles` puede utilizar una consulta Update para sumar un 10% al precio de todos los libros de una editorial determinada.  
  
 Cuando se crea una consulta Update, se especifica:  
  
-   La tabla que se va a actualizar.  
  
-   Las columnas cuyo contenido desea actualizar.  
  
-   El valor o la expresión que se va a utilizar para actualizar cada una de las columnas.  
  
-   Las condiciones de búsqueda que definen las filas que desea actualizar.  
  
 Por ejemplo, la siguiente consulta actualiza la tabla `titles` sumando un 10% al precio de todos los títulos de una editorial:  
  
```  
UPDATE titles  
SET price = price * 1.1  
WHERE (pub_id = '0766')  
```  
  
> [!CAUTION]  
>  No puede deshacer la ejecución de una consulta Update. Como medida de precaución, haga una copia de seguridad de los datos antes de ejecutar la consulta.  
  
### <a name="to-create-an-update-query"></a>Para crear una consulta Update  
  
1.  Agregue en el panel Diagrama la tabla que desea actualizar.  
  
2.  En el menú **Diseñador de consultas** , seleccione **Cambiar tipo**y, a continuación, haga clic en **Actualizar**.  
  
    > [!NOTE]  
    >  Si se muestra más de una tabla en el panel Diagrama al iniciar la consulta Update, el Diseñador de consultas y vistas muestra el [cuadro de diálogo Elegir tabla de destino para Insertar valores](visual-database-tools.md) para solicitarle el nombre de la tabla que se va a actualizar.  
  
3.  En el panel Diagrama, active la casilla de cada columna en la que desea proporcionar nuevos valores. Estas columnas se mostrarán en el panel Criterios. Las columnas se actualizan solo si se agregan a la consulta.  
  
4.  En la columna **Valor nuevo** del panel Criterios, escriba el valor de actualización para la columna. Puede especificar valores literales, nombres de columna o expresiones. El valor debe coincidir (o ser compatible) con el tipo de datos de la columna que va a actualizar.  
  
    > [!CAUTION]  
    >  El Diseñador de consultas y vistas no comprueba si el valor se ajusta al tamaño de la columna que se va a actualizar. Si especifica un valor demasiado largo, se truncará sin previo aviso. Por ejemplo, si una columna `name` tiene una longitud de 20 caracteres y especifica un valor nuevo de 25 caracteres, se cortarán los cinco últimos caracteres.  
  
5.  Defina las filas que desea actualizar especificando condiciones de búsqueda en la columna **Filtro**. Para detalles, consulte [Especificar criterios de búsqueda &#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md).  
  
     Si no especifica ninguna condición de búsqueda, se actualizarán todas las filas de la tabla especificada.  
  
    > [!NOTE]  
    >  Cuando se agrega una columna al panel Criterios para utilizarla en una condición de búsqueda, el Diseñador de consultas y vistas la agrega también a la lista de columnas que se van a actualizar. Si desea utilizar una columna para una condición de búsqueda, pero no quiere actualizarla, desactive la casilla situada junto al nombre de la columna en el rectángulo que representa la tabla o el objeto con valores de tabla.  
  
 Cuando se ejecuta una consulta Update, los resultados no se muestran en el [panel Resultados](results-pane-visual-database-tools.md). En su lugar, aparece un mensaje que indica el número de filas que se han modificado.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de consultas compatibles &#40;Visual Database Tools&#41;](supported-query-types-visual-database-tools.md)   
 [Diseñar temas de procedimientos de consultas y vistas &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [Realizar operaciones básicas con consultas (Visual Database Tools)](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
