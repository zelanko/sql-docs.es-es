---
title: Agregar tablas a las consultas (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- inserting tables
- adding tables
- queries [SQL Server], tables
ms.assetid: 6551aa7e-31a1-4636-852a-819bc53d658b
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: bac26e4bc591867a640fca029e39f94c9ed0a6fe
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2019
ms.locfileid: "65099397"
---
# <a name="add-tables-to-queries-visual-database-tools"></a>Agregar tablas a las consultas (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Cuando crea una consulta, recupera datos de una tabla u otros objetos con estructura de tabla (vistas y determinadas funciones definidas por el usuario). Para trabajar con cualquiera de estos objetos en la consulta, deberá agregarlos al **panel Diagrama**.  
  
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
  
4.  Muestre el **panel SQL** para la consulta interna (la consulta existente que se va a incluir en la nueva consulta externa).  
  
5.  Seleccione todo el texto del **panel SQL**y cópielo en el Portapapeles.  
  
6.  Haga clic en el **panel SQL** de la nueva consulta, coloque el cursor entre los paréntesis agregados y pegue el contenido del Portapapeles.  
  
7.  En el **panel SQL**, agregue un alias después del paréntesis de cierre.  
  
## <a name="see-also"></a>Consulte también  
[Crear alias de tabla &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-table-aliases-visual-database-tools.md)  
[Quitar tablas de las consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/remove-tables-from-queries-visual-database-tools.md)  
[Especificar criterios de búsqueda (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[Resumir los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Realizar operaciones básicas con consultas (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
