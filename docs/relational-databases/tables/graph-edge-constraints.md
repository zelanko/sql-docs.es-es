---
title: Restricciones perimetrales de grafos | Microsoft Docs
ms.custom: ''
ms.date: 04/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- edge constraints [SQL Server]
- CONNECTION constraints
- edge constraints [Azure SQL Database]
- graph edge constraints
- SQL Graph
ms.assetid: ''
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 86544dee5262a1d04c1ff1d8e59f8ddac5e9b5ce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "64774646"
---
# <a name="edge-constraints"></a>Restricciones perimetrales
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  Las restricciones perimetrales se pueden usar para aplicar la integridad de datos y una semántica específica en las tablas perimetrales de una base de datos de gráficos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
  
Este artículo contiene las secciones siguientes.  
  
[Restricciones perimetrales](../../relational-databases/tables/graph-edge-constraints.md#Connection)  

[Restricciones perimetrales](../../relational-databases/tables/graph-edge-constraints.md#Connection)  
  
[Tareas relacionadas](../../relational-databases/tables/graph-edge-constraints.md#Tasks)  
  
##  <a name="Connection"></a> Restricciones perimetrales
 En la primera versión de las características de los gráficos, las tablas perimetrales no aplicaban nada para los puntos de conexión del perímetro. Es decir, los perímetros de una base de datos de gráficos no podían conectar ningún nodo con ninguno otro, independientemente del tipo. 

 Esta versión introduce las restricciones perimetrales, con las que los usuarios pueden agregar restricciones a sus tablas perimetrales, de manera que pueden aplicar una semántica específica y mantener la integridad de datos. Al agregar un perímetro nuevo a una tabla perimetral que tiene restricciones perimetrales, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] exige que los nodos que está intentando conectar el perímetro existan en las tablas de nodo adecuadas. También se garantiza que no se pueda quitar un nodo si un perímetro sigue haciendo referencia a él. 

 ### <a name="edge-constraint-clauses"></a>Cláusulas de restricciones perimetrales
 Cada restricción perimetral consta de una o varias cláusulas de restricción perimetral. Una cláusula de restricción perimetral es el par de nodos FROM y TO a los que el perímetro indicado se ha podido conectar. 

 Imagínese que tiene los nodos `Product` y `Customer` en su gráfico y usa el perímetro `Bought` para conectar estos nodos. La cláusula de restricción perimetral especifica el par de nodos FROM y TO y la dirección del perímetro. En este caso, la cláusula de restricción perimetral será `Customer` TO `Product`. Es decir, se permitirá insertar un perímetro `Bought` que vaya de un `Customer` a un `Product`. Si se intenta insertar un perímetro que vaya de `Product` a `Customer`, se producirá un error. 
  
- Una cláusula de restricción perimetral contiene un par de tablas de nodos FROM y TO donde se aplica la restricción perimetral. 
  
- Los usuarios pueden especificar varias cláusulas de restricción perimetral por restricción perimetral, que se aplicarán como disyunción.

- Si se crean varias restricciones perimetrales en una sola tabla perimetral, los perímetros deberán cumplir TODAS las restricciones para poder ser admitidos.
  
### <a name="indexes-on-edge-constraints"></a>Índices en las restricciones perimetrales
 La creación de una restricción perimetral no crea automáticamente un índice en las columnas `$from_id` y `$to_id` de la tabla perimetral. Se recomienda crear manualmente un índice en un par de columnas `$from_id` y `$to_id` si tiene consultas de búsqueda de puntos o una carga de trabajo OLTP. 

##  <a name="Tasks"></a> Tareas relacionadas  
 En la tabla siguiente se enumeran las tareas comunes asociadas a las restricciones perimetrales.  
  
|Tarea|Artículo|  
|----------|-----------|  
|Describe cómo crear restricciones perimetrales.|[Crear restricciones perimetrales](../../relational-databases/tables/create-edge-constraints.md)|  
|Describe cómo eliminar una restricción perimetral.|[Eliminar una restricción perimetral](../../relational-databases/tables/delete-edge-constraint.md)|  
|Describe cómo modificar una restricción perimetral.|[Modificar una restricción perimetral](../../relational-databases/tables/modify-edge-constraint.md)|  
|Describe cómo ver las propiedades de las restricciones perimetrales.|[Ver propiedades de restricción perimetral](../../relational-databases/tables/view-edge-constraint-properties.md)|  
