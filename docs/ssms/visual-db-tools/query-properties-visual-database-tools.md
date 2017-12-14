---
title: Propiedades de la consulta (Visual Database Tools) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdtsql.chm:69636
- vdt.ppg.querydesigner.query
ms.assetid: 07495669-6ed5-4004-904e-aae1230be5e4
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d7b8519c310eff1942280345c77c630aeea23e56
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="query-properties-visual-database-tools"></a>Propiedades de la consulta (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Estas propiedades aparecen en la ventana Propiedades cuando hay una consulta abierta en Diseñador de consultas y vistas. A menos que se especifique lo contrario, podrá modificar estas propiedades en la ventana Propiedades.  
  
> [!NOTE]  
> Las propiedades de este tema están ordenadas por categoría en lugar de alfabéticamente.  
  
## <a name="options"></a>Opciones  
**Categoría Identidad**  
Se expande para mostrar la propiedad **Nombre** .  
  
**Nombre**  
Muestra el nombre de la consulta actual. No se puede cambiar en [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)].  
  
**Nombre de la base de datos**  
Muestra el nombre del origen de datos de la tabla seleccionada  
  
**Nombre de servidor**  
Muestra el nombre del servidor del origen de datos.  
  
**Diseñador de consultas (Categoría)**  
Se expande para mostrar las propiedades restantes.  
  
**Tabla de destino**  
Especifica el nombre de la tabla en la que se van a insertar los datos. Esta lista se mostrará cuando cree una consulta INSERT o MAKE TABLE. Para las consultas INSERT, seleccione un nombre de tabla de la lista.  
  
En las consultas MAKE TABLE, escriba el nombre de la nueva tabla. Para crear una tabla de destino en otro origen de datos, especifique un nombre de tabla completo, incluido el nombre del origen de datos de destino, el propietario (si fuera necesario) y el nombre de la tabla.  
  
> [!NOTE]  
> El Diseñador de consultas no comprueba si el nombre ya está en uso o si tiene permisos para crear la tabla.  
  
**Valores distintos**  
Especifica que la consulta filtrará los duplicados del conjunto de resultados. Esta opción es útil cuando solo se utilizan algunas columnas de la tabla o tablas y dichas columnas podrían contener valores duplicados, o cuando el proceso de combinar dos o más tablas genera filas duplicadas en el conjunto de resultados. Elegir esta opción equivale a insertar la palabra DISTINCT en la instrucción en el panel SQL.  
  
**Extensión GROUP BY**  
Especifica que las opciones adicionales para consultas basadas en consultas de agregado están disponibles. (Solo se aplica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].)  
  
**Todas las columnas**  
Especifica que se incluirán todas las columnas de todas las tablas de la consulta actual en el conjunto de resultados. La elección de esta opción equivale a especificar en la instrucción SQL un asterisco (*) en lugar de los nombres de columnas individuales a continuación de la palabra clave SELECT.  
  
**Lista de parámetros de la consulta**  
Muestra los parámetros de la consulta. Para editar los parámetros, haga clic en la propiedad y, a continuación, en el botón de puntos suspensivos **(…)** situado a la derecha de la propiedad. (Solo se aplica a OLE DB genérico.)  
  
**Comentario de SQL**  
Muestra una descripción de las instrucciones SQL. Para ver o editar la descripción completa, haga clic en la descripción y después en el botón de puntos suspensivos **(…)** situado a la derecha de la propiedad. Los comentarios pueden incluir información, como quién utiliza la consulta y cuándo. (Solo se aplica a las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 7.0 o versiones posteriores.)  
  
**Especificación superior (Categoría)**  
Se expande para mostrar las propiedades **Superior**, **Porcentaje**, **Expresión**y **Con valores equivalentes** .  
  
**(Superior)**  
Permite especificar que la consulta incluirá una cláusula TOP, que solo devuelve las primeras *n* o el primer *n* por ciento de filas del conjunto de resultados. De forma predeterminada, la consulta devolverá las diez primeras filas del conjunto de resultados.  
  
Utilice este cuadro para cambiar el número de filas que se van a devolver o para especificar un porcentaje diferente. (Solo se aplica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o posterior.)  
  
**Expresión**  
Especifica el número o el porcentaje de filas que la consulta va a devolver. Si establece **Porcentaje** en Sí, este número indicará el porcentaje de filas que devolverá la consulta, mientras que si establece **Porcentaje** en No, representará el número de filas que se devolverá. (Solo se aplica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 7.0 o posterior.)  
  
**Porcentaje**  
Permite especificar que la consulta devolverá solo el primer *n* por ciento de filas del conjunto de resultados. (Solo se aplica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 7.0 o posterior.)  
  
**Con valores equivalentes**  
Especifica que la vista incluirá una cláusula WITH TIES. WITH TIES es útil si una vista incluye una cláusula ORDER BY y una cláusula TOP basadas en un porcentaje. Si se establece esta opción y el límite del porcentaje queda dentro de un conjunto de filas con valores idénticos en la cláusula ORDER BY, se ampliará la vista hasta que incluya todas las filas que faltan. (Solo se aplica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 7.0 o posterior.)  
  
## <a name="see-also"></a>Vea también  
[Realizar consultas con parámetros &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-parameters-visual-database-tools.md)  
[Temas de procedimientos de diseño de consultas y vistas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
