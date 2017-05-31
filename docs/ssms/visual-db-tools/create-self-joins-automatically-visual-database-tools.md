---
title: "Crear autocombinaciones de forma automática (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- automatic joins
- self-joins
- joins [SQL Server], self
ms.assetid: f9ec90e8-3aad-415c-a5c4-8dfa9540e37f
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c25ca1aa33e069fdb08d58196d274aa2198ae3af
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="create-self-joins-automatically-visual-database-tools"></a>Crear autocombinaciones de forma automática (Visual Database Tools)
Si una tabla tiene una relación reflexiva en la base de datos, puede combinarla consigo misma automáticamente.  
  
### <a name="to-create-a-self-join-automatically"></a>Para crear una autocombinación automáticamente  
  
1.  Agregue al [panel Diagrama](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) la tabla con la que desea trabajar.  
  
2.  Vuelva a agregar la misma tabla, de forma que en el panel Diagrama se muestre la misma tabla dos veces.  
  
    El [Diseñador de consultas y vistas](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) asigna un alias a la segunda instancia mediante la adición de un número consecutivo al nombre de tabla. Asimismo, el Diseñador de consultas y vistas crea una línea de combinación entre los dos rectángulos que representan los dos modos diferentes en los que la tabla interviene en la consulta.  
  
## <a name="see-also"></a>Vea también  
[Realizar consultas con combinaciones &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  

