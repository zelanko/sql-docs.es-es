---
title: Tipos de consultas compatibles (Visual Database Tools) | Microsoft Docs
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
- Delete query
- queries [SQL Server], types
- Update query
- Query Designer [SQL Server], query types
- Criteria pane
- Insert Values query
- Select query
- Make Table query
- Insert Results query
- Diagram pane [Visual Database Tools]
- View Designer, query types
ms.assetid: 72b9116c-c128-4078-a78d-257a2955a3f6
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 865bdf79fa72817ed3f3855be855c908d669dd10
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37299425"
---
# <a name="supported-query-types-visual-database-tools"></a>Tipos de consultas compatibles (Visual Database Tools)
  Puede crear los siguientes tipos de consulta en los paneles Diagrama y Criterios (paneles gráficos) del [Diseñador de consultas y vistas](visual-database-tools.md):  
  
-   **Consulta Select** Recupera datos de una o más tablas o vistas. Este tipo de consulta crea una instrucción SQL SELECT.  
  
-   **Insertar resultados** Crea filas nuevas mediante la copia de filas existentes de una tabla a otra, o a la misma tabla como nuevas filas. Este tipo de consulta crea una instrucción SQL INSERT INTO...SELECT.  
  
-   **Insertar valores** Crea una nueva fila e inserta valores en columnas especificadas. Este tipo de consulta crea una instrucción SQL INSERT INTO...VALUES.  
  
-   **Consulta de actualización** Cambia los valores de columnas individuales de una o más filas existentes en una tabla. Este tipo de consulta crea una instrucción SQL UPDATE...SET.  
  
-   **Consulta de eliminación** Quita una o más filas de una tabla. Este tipo de consulta crea una instrucción SQL DELETE.  
  
    > [!NOTE]  
    >  Una consulta Delete quita filas completas de la tabla. Si desea eliminar valores de columnas de datos individuales, utilice una consulta Update.  
  
-   **Consulta de creación de tabla** Crea una nueva tabla y crea filas en ella copiando los resultados de una consulta en la misma. Este tipo de consulta crea una instrucción SQL SELECT...INTO.  
  
 Además de las consultas que puede crear mediante el uso de los paneles gráficos, puede especificar cualquier instrucción SQL en el panel SQL, como consultas de unión.  
  
 Cuando crea consultas mediante instrucciones SQL que no puedan representarse en los paneles gráficos, el Diseñador de consultas y vistas atenúa esos paneles para indicar que no reflejan la consulta que está creando. Sin embargo, los paneles atenuados están activos todavía y, en muchos casos, puede realizar cambios en la consulta en esos paneles. Si los cambios que realiza tienen como resultado una consulta que puede representarse en los paneles gráficos, esos paneles ya no estarán atenuados.  
  
## <a name="see-also"></a>Vea también  
 [Diseñar temas de procedimientos de consultas y vistas &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [Tipos de consultas (Visual Database Tools)](types-of-queries-visual-database-tools.md)  
  
  
