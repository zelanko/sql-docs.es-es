---
title: Crear consultas de inserción de valores (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- inserting values
- queries [SQL Server], types
- adding values
- row additions [SQL Server], Insert Values query
- inserting rows
- Insert Values query
- adding rows
- table values [SQL Server]
ms.assetid: 2d4b2f6d-cc09-434b-8a0e-ccce40628064
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: f819a9ef1dacf7247c318ff90be5036579e2882d
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2019
ms.locfileid: "67687756"
---
# <a name="create-insert-values-queries-visual-database-tools"></a>Crear consultas de inserción de valores (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Puede crear una nueva fila en la tabla actual mediante una consulta de inserción de valores. Cuando se crea una consulta de inserción de valores, se especifica:  
  
-   La tabla de base de datos a la que se va a agregar la fila.  
  
-   Las columnas cuyo contenido desea agregar.  
  
-   El valor o la expresión que se va a insertar en las distintas columnas.  
  
Por ejemplo, en la siguiente consulta se agrega una fila a la tabla `titles` , que especifica valores para el título, el tipo, la editorial y el precio:  
  
```  
INSERT INTO titles  
         (title_id, title, type, pub_id, price)  
VALUES   ('BU9876', 'Creating Web Pages', 'business', '1389', '29.99')  
```  
  
Cuando se crea una consulta de inserción de valores, el panel Criterios cambia para reflejar las únicas opciones disponibles para insertar una nueva fila: el nombre de columna y el valor que se va a insertar.  
  
> [!CAUTION]  
> No se puede deshacer la operación de ejecutar una consulta de inserción de valores. Como medida de precaución, haga una copia de seguridad de los datos antes de ejecutar la consulta.  
  
### <a name="to-create-an-insert-values-query"></a>Para crear una Consulta de inserción de valores  
  
1.  Agregue en el panel Diagrama la tabla que desea actualizar.  
  
2.  En el menú **Diseñador de consultas** , seleccione **Cambiar tipo**y, a continuación, haga clic en **Insertar valores**.  
  
    > [!NOTE]  
    > Si aparece más de una tabla en el panel Diagrama al iniciar la consulta de inserción de valores, el Diseñador de consultas y vistas mostrará el [cuadro de diálogo Elegir tabla de destino para Insertar valores](../../ssms/visual-db-tools/choose-target-table-for-insert-values-dialog-box-visual-database-tools.md) para solicitarle el nombre de la tabla que se va a actualizar.  
  
3.  En el panel Diagrama, active la casilla de cada columna en la que desea proporcionar nuevos valores. Estas columnas se mostrarán en el panel Criterios. Las columnas se actualizan solo si se agregan a la consulta.  
  
4.  En la columna **Valor nuevo** del panel Criterios, escriba el nuevo valor para la columna. Puede especificar valores literales, nombres de columna o expresiones. El valor debe coincidir (o ser compatible) con el tipo de datos de la columna que va a actualizar.  
  
    > [!CAUTION]  
    > El Diseñador de consultas y vistas no puede comprobar si el valor se ajusta al tamaño de la columna que se va a insertar. Si especifica un valor demasiado largo, se truncará sin previo aviso. Por ejemplo, si una columna `name` tiene una longitud de 20 caracteres y especifica un valor de inserción de 25 caracteres, se cortarán los cinco últimos caracteres.  
  
Cuando se ejecuta una consulta de inserción de valores, los resultados no se muestran en el [panel Resultados](../../ssms/visual-db-tools/results-pane-visual-database-tools.md). En su lugar, aparece un mensaje que indica el número de filas que se han modificado.  
  
## <a name="see-also"></a>Consulte también  
[Tipos de consultas compatibles &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[Temas de procedimientos de diseño de consultas y vistas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Realizar operaciones básicas con consultas (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
