---
description: Crear autocombinaciones de forma automática (Visual Database Tools)
title: Crear autocombinaciones automáticamente
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- automatic joins
- self-joins
- joins [SQL Server], self
ms.assetid: f9ec90e8-3aad-415c-a5c4-8dfa9540e37f
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 3792e29ae83d28e8c695cfebbd5fc086fe4c267b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468393"
---
# <a name="create-self-joins-automatically-visual-database-tools"></a>Crear autocombinaciones de forma automática (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Si una tabla tiene una relación reflexiva en la base de datos, puede combinarla consigo misma automáticamente.  
  
### <a name="to-create-a-self-join-automatically"></a>Para crear una autocombinación automáticamente  
  
1.  Agregue al [panel Diagrama](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) la tabla con la que desea trabajar.  
  
2.  Vuelva a agregar la misma tabla, de forma que en el panel Diagrama se muestre la misma tabla dos veces.  
  
    El [Diseñador de consultas y vistas](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) asigna un alias a la segunda instancia mediante la adición de un número consecutivo al nombre de tabla. Asimismo, el Diseñador de consultas y vistas crea una línea de combinación entre los dos rectángulos que representan los dos modos diferentes en los que la tabla interviene en la consulta.  
  
## <a name="see-also"></a>Consulte también  
[Realizar consultas con combinaciones &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
