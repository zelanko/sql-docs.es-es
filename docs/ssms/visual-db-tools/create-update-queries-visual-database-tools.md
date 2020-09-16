---
description: Crear consultas de actualización (Visual Database Tools)
title: Crear consultas de actualización
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- tables [SQL Server], updating
- queries [SQL Server], types
- Update query
- updating tables
ms.assetid: 178b7b75-8078-4e61-b2a8-4719b9d8033d
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: f750573b4afb02cd06f3ee1a8c17008639910608
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462826"
---
# <a name="create-update-queries-visual-database-tools"></a>Crear consultas de actualización (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
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
> No puede deshacer la ejecución de una consulta Update. Como medida de precaución, haga una copia de seguridad de los datos antes de ejecutar la consulta.  
  
### <a name="to-create-an-update-query"></a>Para crear una consulta Update  
  
1.  Agregue en el panel Diagrama la tabla que desea actualizar.  
  
2.  En el menú **Diseñador de consultas** , seleccione **Cambiar tipo**y, a continuación, haga clic en **Actualizar**.  
  
    > [!NOTE]  
    > Si se muestra más de una tabla en el panel Diagrama al iniciar la consulta Update, el Diseñador de consultas y vistas muestra el [cuadro de diálogo Elegir tabla de destino para Insertar valores](../../ssms/visual-db-tools/choose-target-table-for-insert-values-dialog-box-visual-database-tools.md) para solicitarle el nombre de la tabla que se va a actualizar.  
  
3.  En el panel Diagrama, active la casilla de cada columna en la que desea proporcionar nuevos valores. Estas columnas se mostrarán en el panel Criterios. Las columnas se actualizan solo si se agregan a la consulta.  
  
4.  En la columna **Valor nuevo** del panel Criterios, escriba el valor de actualización para la columna. Puede especificar valores literales, nombres de columna o expresiones. El valor debe coincidir (o ser compatible) con el tipo de datos de la columna que va a actualizar.  
  
    > [!CAUTION]  
    > El Diseñador de consultas y vistas no comprueba si el valor se ajusta al tamaño de la columna que se va a actualizar. Si especifica un valor demasiado largo, se truncará sin previo aviso. Por ejemplo, si una columna `name` tiene una longitud de 20 caracteres y especifica un valor nuevo de 25 caracteres, se cortarán los cinco últimos caracteres.  
  
5.  Defina las filas que desea actualizar especificando condiciones de búsqueda en la columna **Filtro**. Para detalles, consulte [Especificar criterios de búsqueda &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md).  
  
    Si no especifica ninguna condición de búsqueda, se actualizarán todas las filas de la tabla especificada.  
  
    > [!NOTE]  
    > Cuando se agrega una columna al panel Criterios para utilizarla en una condición de búsqueda, el Diseñador de consultas y vistas la agrega también a la lista de columnas que se van a actualizar. Si desea utilizar una columna para una condición de búsqueda, pero no quiere actualizarla, desactive la casilla situada junto al nombre de la columna en el rectángulo que representa la tabla o el objeto con valores de tabla.  
  
Cuando se ejecuta una consulta Update, los resultados no se muestran en el [panel Resultados](../../ssms/visual-db-tools/results-pane-visual-database-tools.md). En su lugar, aparece un mensaje que indica el número de filas que se han modificado.  
  
## <a name="see-also"></a>Consulte también  
[Tipos de consultas compatibles &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[Temas de procedimientos de diseño de consultas y vistas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Realizar operaciones básicas con consultas (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
