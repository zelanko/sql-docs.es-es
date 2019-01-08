---
title: Propiedades de la consulta (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:69636
- vdt.ppg.querydesigner.query
ms.assetid: 07495669-6ed5-4004-904e-aae1230be5e4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6e9232f5de2172c7dfbe503a26188fdf4d05550c
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52759965"
---
# <a name="query-properties-visual-database-tools"></a>Propiedades de la consulta (Visual Database Tools)
  Estas propiedades aparecen en la ventana Propiedades cuando hay una consulta abierta en el Diseñador de consultas y vistas. A menos que se especifique lo contrario, podrá modificar estas propiedades en la ventana Propiedades.  
  
> [!NOTE]  
>  Las propiedades de este tema están ordenadas por categoría en lugar de alfabéticamente.  
  
## <a name="options"></a>Opciones  
 **Categoría Identidad**  
 Se expande para mostrar la propiedad **Nombre** .  
  
 **Name**  
 Muestra el nombre de la consulta actual. No se puede cambiar en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 **Database Name**  
 Muestra el nombre del origen de datos de la tabla seleccionada  
  
 **Nombre de servidor**  
 Muestra el nombre del servidor del origen de datos.  
  
 **Diseñador de consultas (Categoría)**  
 Se expande para mostrar las propiedades restantes.  
  
 **Tabla de destino**  
 Especifica el nombre de la tabla en la que se van a insertar los datos. Esta lista se mostrará cuando cree una consulta INSERT o MAKE TABLE. Para las consultas INSERT, seleccione un nombre de tabla de la lista.  
  
 En las consultas MAKE TABLE, escriba el nombre de la nueva tabla. Para crear una tabla de destino en otro origen de datos, especifique un nombre de tabla completo, incluido el nombre del origen de datos de destino, el propietario (si fuera necesario) y el nombre de la tabla.  
  
> [!NOTE]  
>  El Diseñador de consultas no comprueba si el nombre ya está en uso o si tiene permisos para crear la tabla.  
  
 **Valores distintos**  
 Especifica que la consulta filtrará los duplicados del conjunto de resultados. Esta opción es útil cuando solo se utilizan algunas columnas de la tabla o tablas y dichas columnas podrían contener valores duplicados, o cuando el proceso de combinar dos o más tablas genera filas duplicadas en el conjunto de resultados. Elegir esta opción equivale a insertar la palabra DISTINCT en la instrucción en el panel SQL.  
  
 **Extensión GROUP BY**  
 Especifica que las opciones adicionales para consultas basadas en consultas de agregado están disponibles. (Solo se aplica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].)  
  
 **Todas las columnas**  
 Especifica que se incluirán todas las columnas de todas las tablas de la consulta actual en el conjunto de resultados. La elección de esta opción equivale a especificar en la instrucción SQL un asterisco (*) en lugar de los nombres de columnas individuales a continuación de la palabra clave SELECT.  
  
 **Lista de parámetros de la consulta**  
 Muestra los parámetros de la consulta. Para editar los parámetros, haga clic en la propiedad y, después, en el botón de puntos suspensivos **(...)** situado a la derecha de la propiedad. (Solo se aplica a OLE DB genérico.)  
  
 **Comentario de SQL**  
 Muestra una descripción de las instrucciones SQL. Para ver o editar la descripción completa, haga clic en la descripción y después en el botón de puntos suspensivos **(...)** situado a la derecha de la propiedad. Los comentarios pueden incluir información, como quién utiliza la consulta y cuándo. (Solo se aplica a las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 o versiones posteriores.)  
  
 **Especificación superior (Categoría)**  
 Se expande para mostrar las propiedades **Superior**, **Porcentaje**, **Expresión**y **Con valores equivalentes** .  
  
 **(Superior)**  
 Permite especificar que la consulta incluirá una cláusula TOP, que solo devuelve las primeras *n* o el primer *n* por ciento de filas del conjunto de resultados. De forma predeterminada, la consulta devolverá las diez primeras filas del conjunto de resultados.  
  
 Utilice este cuadro para cambiar el número de filas que se van a devolver o para especificar un porcentaje diferente. (Solo se aplica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o posterior.)  
  
 **Expresión**  
 Especifica el número o el porcentaje de filas que la consulta va a devolver. Si establece **Porcentaje** en Sí, este número indicará el porcentaje de filas que devolverá la consulta, mientras que si establece **Porcentaje** en No, representará el número de filas que se devolverá. (Solo se aplica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 o posterior.)  
  
 **Porcentaje**  
 Permite especificar que la consulta devolverá solo el primer *n* por ciento de filas del conjunto de resultados. (Solo se aplica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 o posterior.)  
  
 **Con valores equivalentes**  
 Especifica que la vista incluirá una cláusula WITH TIES. WITH TIES es útil si una vista incluye una cláusula ORDER BY y una cláusula TOP basadas en un porcentaje. Si se establece esta opción y el límite del porcentaje queda dentro de un conjunto de filas con valores idénticos en la cláusula ORDER BY, se ampliará la vista hasta que incluya todas las filas que faltan. (Solo se aplica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 o posterior.)  
  
## <a name="see-also"></a>Vea también  
 [Consulta con parámetros &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Temas de procedimientos de diseño de consultas y vistas &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
