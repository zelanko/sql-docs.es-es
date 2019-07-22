---
title: Agregar tablas derivadas a las consultas (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- queries [Visual Database Tools]
- joins [SQL Server], derived tables
- table joins [SQL Server]
- derived tables
ms.assetid: 05f1ba1d-465f-4e36-84bb-21b963c9b8f9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: da76d9e2f82f832e5426522047caa01d76262e39
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263350"
---
# <a name="add-derived-tables-to-queries-visual-database-tools"></a>Agregar tablas derivadas a las consultas (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Las tablas derivadas son conjuntos de resultados que se utilizan como orígenes de tabla en una consulta. Puede agregar una tabla derivada a una consulta en el **panel Diagrama**.  
  
### <a name="to-add-a-derived-table-to-a-query"></a>Para agregar una tabla derivada a una consulta  
  
1.  Abra una consulta existente o cree una nueva.  
  
2.  Haga clic con el botón derecho en el **panel Diagrama** y elija **Agregar nueva tabla derivada**.  
  
    Se agrega una nueva tabla con el nombre derivedtbl_*N* y la instrucción SELECT de la tabla derivada se agrega a la cláusula FROM de la consulta.  
  
## <a name="see-also"></a>Consulte también  
[Realizar operaciones básicas con consultas (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
[Crear consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-queries-visual-database-tools.md)  
[Abrir consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/open-queries-visual-database-tools.md)  
[SELECT (Transact-SQL)](https://msdn.microsoft.com/dc85caea-54d1-49af-b166-f3aa2f3a93d0)  
  
