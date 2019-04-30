---
title: Crear consultas con parámetros sin nombre (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- unnamed parameters
- parameters [SQL Server], unnamed
ms.assetid: 5f4b664b-3d3d-4d07-a0e7-791d78743504
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f9eebede28d257083b55ffd4b14943b7ebc1a95b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63184336"
---
# <a name="create-queries-with-unnamed-parameters-visual-database-tools"></a>Crear consultas con parámetros sin nombre (Visual Database Tools)
  Puede crear una consulta con un parámetro sin nombre incluyendo un signo de interrogación (?) como marcador de posición para un valor literal. El Diseñador de consultas y vistas le asignará un nombre temporal. Puede especificar tantos parámetros sin nombre como necesite en la consulta.  
  
 Cuando se ejecute la consulta en el Diseñador de consultas y vistas, se mostrará el cuadro de diálogo Parámetros de la consulta con el nombre temporal.  
  
### <a name="to-specify-an-unnamed-parameter"></a>Para especificar un parámetro sin nombre  
  
1.  Agregue las columnas o expresiones que desea buscar al [panel Criterios](visual-database-tools.md). Si no desea que las columnas o expresiones de búsqueda aparezcan en los resultados de la consulta, quítelas como columnas de resultados.  
  
2.  Busque la fila que contiene la columna de datos o expresión que va a buscar y, luego, en la columna de cuadrícula **Filtro** , escriba un signo de interrogación (?).  
  
     De forma predeterminada, el Diseñador de consultas y vistas agrega el operador "=". No obstante, puede editar la celda para sustituir el operador por ">", "<" o cualquier otro operador de comparación SQL.  
  
## <a name="see-also"></a>Vea también  
 [Realizar consultas con parámetros &#40;Visual Database Tools&#41;](query-with-parameters-visual-database-tools.md)  
  
  
