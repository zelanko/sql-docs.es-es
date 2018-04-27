---
title: Excluir filas duplicadas (Visual Database Tools) | Microsoft Docs
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
- search criteria [SQL Server], excluding rows
- row duplicates [SQL Server]
- duplicate rows
- row excluded in search [SQL Server]
- result sets [SQL Server], duplicate values
- excluding rows
ms.assetid: ab35a363-421d-4665-946b-ae3f6397af50
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 314556d85b57f20e05f91aa1e0d18735ee6a520e
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="exclude-duplicate-rows-visual-database-tools"></a>Excluir filas duplicadas (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Si solo desea ver los valores únicos de un conjunto de resultados, puede indicar que se excluyan los duplicados del conjunto de resultados.  
  
### <a name="to-exclude-duplicate-rows-from-the-result-set"></a>Para excluir filas duplicadas del conjunto de resultados  
  
1.  Haga clic con el botón derecho en el fondo del panel Diagrama y, luego, elija **Propiedades** en el menú contextual.  
  
2.  En la ventana Propiedades, haga clic en **Valores DISTINCT** y establezca el valor en **Sí**.  
  
    El Diseñador de consultas y vistas inserta la palabra clave DISTINCT delante de la lista de columnas mostradas en la instrucción SQL.  
  
    > [!NOTE]  
    > Si utiliza la palabra clave DISTINCT , es posible que no pueda modificar el conjunto de resultados en el panel de resultados.  
  
## <a name="see-also"></a>Ver también  
[Especificar criterios de búsqueda (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[Ordenar y agrupar los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  
