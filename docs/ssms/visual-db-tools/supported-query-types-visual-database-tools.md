---
title: Tipos de consultas compatibles (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e7a4cc3ee7fd07d60c452809a285e4369c603df6
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="supported-query-types-visual-database-tools"></a>Tipos de consultas compatibles (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Puede crear los siguientes tipos de consulta en los paneles Diagrama y Criterios (paneles gráficos) del [Diseñador de consultas y vistas](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md):  
  
-   **Consulta Select** Recupera datos de una o más tablas o vistas. Este tipo de consulta crea una instrucción SQL SELECT.  
  
-   **Insertar resultados** Crea filas nuevas mediante la copia de filas existentes de una tabla a otra, o a la misma tabla como nuevas filas. Este tipo de consulta crea una instrucción SQL INSERT INTO...SELECT.  
  
-   **Insertar valores** Crea una nueva fila e inserta valores en columnas especificadas. Este tipo de consulta crea una instrucción SQL INSERT INTO...VALUES.  
  
-   **Consulta de actualización** Cambia los valores de columnas individuales de una o más filas existentes en una tabla. Este tipo de consulta crea una instrucción SQL UPDATE...SET.  
  
-   **Consulta de eliminación** Quita una o más filas de una tabla. Este tipo de consulta crea una instrucción SQL DELETE.  
  
    > [!NOTE]  
    > Una consulta Delete quita filas completas de la tabla. Si desea eliminar valores de columnas de datos individuales, utilice una consulta Update.  
  
-   **Consulta de creación de tabla** Crea una nueva tabla y crea filas en ella copiando los resultados de una consulta en la misma. Este tipo de consulta crea una instrucción SQL SELECT...INTO.  
  
Además de las consultas que puede crear mediante el uso de los paneles gráficos, puede especificar cualquier instrucción SQL en el panel SQL, como consultas de unión.  
  
Cuando crea consultas mediante instrucciones SQL que no puedan representarse en los paneles gráficos, el Diseñador de consultas y vistas atenúa esos paneles para indicar que no reflejan la consulta que está creando. Sin embargo, los paneles atenuados están activos todavía y, en muchos casos, puede realizar cambios en la consulta en esos paneles. Si los cambios que realiza tienen como resultado una consulta que puede representarse en los paneles gráficos, esos paneles ya no estarán atenuados.  
  
## <a name="see-also"></a>Ver también  
[Temas de procedimientos de diseño de consultas y vistas (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Tipos de consultas (Visual Database Tools)](../../ssms/visual-db-tools/types-of-queries-visual-database-tools.md)  
  
