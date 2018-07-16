---
title: Agregar tablas a las consultas (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- inserting tables
- adding tables
- queries [SQL Server], tables
ms.assetid: 6551aa7e-31a1-4636-852a-819bc53d658b
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 208ed8613c10ffb0408a471ffd9ca66180f07d59
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37312855"
---
# <a name="add-tables-to-queries-visual-database-tools"></a>Agregar tablas a las consultas (Visual Database Tools)
  Cuando crea una consulta, va a recuperar datos de una tabla u otros objetos con estructura de tabla (vistas y determinadas funciones definidas por el usuario). Para trabajar con cualquiera de estos objetos en la consulta, deberá agregarlos al **panel Diagrama**.  
  
### <a name="to-add-a-table-or-table-valued-object-to-a-query"></a>Para agregar una tabla u objeto con valor de tabla a una consulta  
  
1.  Haga clic con el botón derecho en el fondo del **panel Diagrama** del Diseñador de consultas y vistas y, a continuación, elija **Agregar tabla** en el menú contextual.  
  
2.  En el cuadro de diálogo **Agregar tabla** , seleccione la pestaña correspondiente al tipo de objeto que desea agregar a la consulta.  
  
3.  En la lista de elementos, haga doble clic en cada elemento que desee agregar.  
  
4.  Cuando acabe de agregar elementos, haga clic en **Cerrar**.  
  
     El Diseñador de consultas y vistas actualizará el **panel Diagrama**, el **panel Criterios**y el **panel SQL** en consecuencia.  
  
 Cuando haga referencia a tablas o vistas en la instrucción del panel SQL, se agregarán automáticamente a la consulta.  
  
 El Diseñador de consultas y vistas no mostrará las columnas de datos de una tabla o de un objeto con estructura de tabla si no tiene suficientes derechos de acceso o si el proveedor no puede devolver información acerca de la tabla o del objeto. En este caso, solo se muestra una barra de título y la casilla * (Todas las columnas) en la tabla o el objeto con valores de tabla.  
  
### <a name="to-add-an-existing-query-to-a-new-query"></a>Para agregar una consulta existente a una consulta nueva  
  
1.  Compruebe que el **panel SQL** está visible en la nueva consulta que va a crear.  
  
2.  En el **panel SQL**, escriba un paréntesis de apertura y otro de cierre () después de la palabra FROM.  
  
3.  Abra el Diseñador de consultas para la consulta existente. (Ahora tiene dos Diseñadores de consultas abiertos.)  
  
4.  Muestre el **panel SQL** para la consulta interna (la consulta existente que va a incluir en la nueva consulta externa).  
  
5.  Seleccione todo el texto del **panel SQL**y cópielo en el Portapapeles.  
  
6.  Haga clic en el **panel SQL** de la nueva consulta, coloque el cursor entre los paréntesis agregados y pegue el contenido del Portapapeles.  
  
7.  En el **panel SQL**, agregue un alias después del paréntesis de cierre.  
  
## <a name="see-also"></a>Vea también  
 [Crear alias de tabla &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Quitar tablas de las consultas &#40;Visual Database Tools&#41;](remove-tables-from-queries-visual-database-tools.md)   
 [Especificar criterios de búsqueda &#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)   
 [Resumir los resultados de consulta &#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md)   
 [Realizar operaciones básicas con consultas (Visual Database Tools)](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
