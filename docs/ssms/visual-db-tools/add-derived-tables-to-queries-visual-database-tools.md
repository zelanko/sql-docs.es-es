---
title: Agregar tablas derivadas a consultas
ms.prod: sql
ms.prod_service: sql-tools
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
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: b36b4774386343ee691cfa455787cf093639ce07
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "75253442"
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
  
