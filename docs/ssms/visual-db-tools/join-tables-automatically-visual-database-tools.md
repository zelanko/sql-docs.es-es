---
title: Combinar tablas automáticamente (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- automatic joins
- joins [SQL Server], creating
- joins [SQL Server], automatic
ms.assetid: f152af82-bcb6-49ca-af19-48cdb7fc9ac6
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a6026bee9d0e1bea2a57423664d42a730b6332f0
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38023701"
---
# <a name="join-tables-automatically-visual-database-tools"></a>Combinar tablas automáticamente (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Al agregar dos o más tablas a una consulta, el [Diseñador de consultas y vistas](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) intenta determinar si están relacionadas. Si lo están, el Diseñador de consultas y vistas coloca automáticamente líneas de combinación entre los rectángulos que representan las tablas o los objetos con estructura de tabla.  
  
El Diseñador de consultas y vistas determinará que las tablas están combinadas si:  
  
-   La base de datos contiene información que especifica que las tablas están relacionadas.  
  
-   Dos columnas, una en cada tabla, tienen el mismo nombre y tipo de datos. La columna debe ser una clave principal en al menos una de las tablas. Por ejemplo, al agregar las tablas `employee` y `jobs` , si la columna `job_id` es la clave principal de la tabla `jobs` y cada tabla tiene una columna llamada `job_id` con el mismo tipo de datos, el Diseñador de consultas y vistas combinará automáticamente las tablas.  
  
    > [!NOTE]  
    > El Diseñador de consultas y vistas creará solo una combinación basada en columnas con el mismo nombre y tipo de datos. Si son posibles varias combinaciones, el Diseñador de consultas y vistas se detendrá después de crear una combinación basada en el primer conjunto de columnas coincidentes que encuentre.  
  
-   El Diseñador de consultas y vistas detecta que una condición de búsqueda (una cláusula WHERE) es realmente una condición de combinación. Por ejemplo, puede agregar las tablas `employee` y `jobs`y crear, a continuación, una condición de búsqueda que busque el mismo valor en la columna `job_id` de ambas tablas. En este caso, el Diseñador de consultas y vistas detecta que la condición de búsqueda genera una combinación y, a continuación, crea una condición de combinación a partir de la condición de búsqueda.  
  
Si el Diseñador de consultas y vistas ha creado una combinación que no es adecuada para la consulta, puede modificarla o quitarla. Para detalles, consulte [Modificar operadores de combinación &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/modify-join-operators-visual-database-tools.md) y [Quitar combinaciones &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/remove-joins-visual-database-tools.md).  
  
Si el Diseñador de consultas y vistas no combina automáticamente las tablas de la consulta, puede crear una combinación de forma manual. Para detalles, consulte [Combinar tablas manualmente &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-manually-visual-database-tools.md).  
  
## <a name="see-also"></a>Ver también  
[Cómo representa combinaciones el Diseñador de consultas y vistas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/how-the-query-and-view-designer-represents-joins-visual-database-tools.md)  
[Temas de procedimientos de diseño de consultas y vistas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Realizar consultas con combinaciones &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
