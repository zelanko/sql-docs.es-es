---
title: Crear autocombinaciones de forma automática (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- automatic joins
- self-joins
- joins [SQL Server], self
ms.assetid: f9ec90e8-3aad-415c-a5c4-8dfa9540e37f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4a428a44d33b5990e849772b43841df472ca7f6c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058075"
---
# <a name="create-self-joins-automatically-visual-database-tools"></a>Crear autocombinaciones de forma automática (Visual Database Tools)
  Si una tabla tiene una relación reflexiva en la base de datos, puede combinarla consigo misma automáticamente.  
  
### <a name="to-create-a-self-join-automatically"></a>Para crear una autocombinación automáticamente  
  
1.  Agregue al [panel Diagrama](visual-database-tools.md) la tabla con la que desea trabajar.  
  
2.  Vuelva a agregar la misma tabla, de forma que en el panel Diagrama se muestre la misma tabla dos veces.  
  
     El [Diseñador de consultas y vistas](query-and-view-designer-tools-visual-database-tools.md) asigna un alias a la segunda instancia mediante la adición de un número consecutivo al nombre de tabla. Asimismo, el Diseñador de consultas y vistas crea una línea de combinación entre los dos rectángulos que representan los dos modos diferentes en los que la tabla interviene en la consulta.  
  
## <a name="see-also"></a>Consulte también  
 [Realizar consultas con combinaciones &#40;Visual Database Tools&#41;](query-with-joins-visual-database-tools.md)  
  
  
