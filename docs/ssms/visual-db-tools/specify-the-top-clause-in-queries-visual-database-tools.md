---
title: Especificar la cláusula TOP en las consultas
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- TOP clause, queries
- percentage of rows returned [SQL Server]
- number of rows
- search conditions [SQL Server], TOP clause
- restricting rows returned
- search criteria [SQL Server], limiting rows returned
- inspecting portion of results
- limiting rows returned
- search criteria [SQL Server], TOP clause
ms.assetid: ba7d7c10-9bb3-4d9b-90b0-5fa94ecae59b
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: 7995bd9ac78595200f6ded5e23c0f0b40cf3ff66
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "75254931"
---
# <a name="specify-the-top-clause-in-queries-visual-database-tools"></a>Especificar la cláusula TOP en consultas (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
La cláusula TOP devuelve solo las primeras *n* o *n percent* filas de una consulta. La cláusula TOP resulta muy útil si se desea inspeccionar una parte de los resultados para averiguar si el funcionamiento de la consulta es el esperado, sin tener que emplear los recursos necesarios para devolver todos los resultados de la consulta.  
  
### <a name="to-specify-the-top-clause-in-queries"></a>Para especificar la cláusula TOP en las consultas  
  
1.  Abra una consulta del Explorador de soluciones o cree una nueva.  
  
2.  En el menú **Ver** , haga clic en **Ventana Propiedades**.  
  
3.  En la **Ventana Propiedades**, busque y expanda la propiedad **Especificación superior** .  
  
4.  Haga clic en la propiedad secundaria **(Superior)** y establézcala en **Sí**.  
  
5.  En la propiedad secundaria **Expresión** , escriba una expresión que tenga un resultado numérico (por ejemplo, "10" o "2*5").  
  
6.  Haga clic en la propiedad secundaria **Porcentaje** e indique si la propiedad **Expresión** debe tratarse como un porcentaje de todas las filas devueltas (Sí) o como el número absoluto de filas devueltas (No).  
  
7.  Si la consulta utiliza la cláusula ORDER BY, haga clic en la propiedad secundaria **Con valores equivalentes** y elija **Sí** para mostrar todas las filas de un grupo si solo parte del grupo está incluida o **No** para truncarlos.  
  
Al realizar el procedimiento anterior, observe que la cláusula TOP que se muestra en el panel SQL cambia para reflejar la configuración actual de las propiedades.  
  
> [!NOTE]  
> También puede cambiar los valores de las propiedades secundarias de **Especificación superior** editando el cláusula TOP en el panel SQL.  
  
## <a name="see-also"></a>Consulte también  
[Temas de procedimientos de diseño de consultas y vistas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Propiedades de la consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-properties-visual-database-tools.md)  
  
