---
title: Crear consultas de búsqueda de texto completo (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- CONTAINS predicate (Transact-SQL)
- queries [full-text search], creating
- full-text queries [SQL Server], creating
ms.assetid: 537fa556-390e-4c88-9b8e-679848d94abc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1f3ab74c6dd095fd92e0f9d20ba622be70a37ef9
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52768577"
---
# <a name="create-full-text-search-queries-visual-database-tools"></a>Crear consultas de búsqueda de texto completo (Visual Database Tools)
  Las búsquedas de texto completo utilizan el predicado CONTAINS para buscar las filas que contienen el texto especificado en una determinada columna. Las búsquedas de texto completo solo pueden realizarse en las columnas que tienen índices de texto completo activos. Si intenta utilizar la cláusula CONTAINS en una columna que no tiene un índice de texto completo activo, recibirá un error. Para obtener más información sobre los índices de texto completo y la cláusula CONTAINS, consulte [Full-Text Search](../../relational-databases/search/full-text-search.md) y [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql).  
  
### <a name="to-create-a-full-text-search-query"></a>Para crear una consulta de búsqueda de texto completo  
  
1.  Abra una consulta del Explorador de soluciones o cree una nueva.  
  
2.  Utilice la función CONTAINS en la cláusula WHERE de su consulta para buscar una columna de texto completo.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de consultas compatibles &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Diseñar temas de procedimientos de consultas y vistas &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [Realizar operaciones básicas con consultas (Visual Database Tools)](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
