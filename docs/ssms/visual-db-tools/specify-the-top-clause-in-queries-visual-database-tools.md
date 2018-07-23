---
title: Especificar la cláusula TOP en consultas (Visual Database Tools) | Microsoft Docs
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
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1bcf376898866238839c0658d9b445e11b05c70e
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38023600"
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
  
## <a name="see-also"></a>Ver también  
[Temas de procedimientos de diseño de consultas y vistas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Propiedades de la consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-properties-visual-database-tools.md)  
  
