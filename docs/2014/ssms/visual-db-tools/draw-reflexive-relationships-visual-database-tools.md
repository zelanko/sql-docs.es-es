---
title: Dibujar relaciones reflexivas (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- drawing reflexive relationships
- reflexive relationships
- database diagrams [SQL Server], relationships
ms.assetid: e218363f-faec-46d5-9904-a537fbcc994d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c11f414bded0c0b927579eb5dbec4664584a055e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52750497"
---
# <a name="draw-reflexive-relationships-visual-database-tools"></a>Dibujar relaciones reflexivas (Visual Database Tools)
  Puede crear una relación reflexiva para vincular una o más columnas de una tabla con una o más columnas de la misma tabla. Por ejemplo, suponga que la tabla `employee` contiene una columna `emp_id` y una columna `mgr_id` . Como cada director también es un empleado, para relacionar estas dos columnas debe dibujar una línea de relación desde la tabla hasta la propia tabla. Esta relación garantiza que cada Id. de director que se agregue a la tabla coincida con un Id. de empleado existente.  
  
 Antes de crear una relación debe definir una restricción PRIMARY KEY o UNIQUE para la tabla. Después debe relacionar la columna de clave principal con una columna coincidente. Cuando haya creado la relación, la columna coincidente se convertirá en una clave externa de la tabla.  
  
### <a name="to-draw-a-reflexive-relationship"></a>Para dibujar una relación reflexiva  
  
1.  En el diagrama de base de datos, haga clic en el selector de fila de la columna de base de datos que desea relacionar con otra columna y arrastre el puntero fuera de la tabla hasta que aparezca una línea.  
  
2.  Arrastre la línea hasta la tabla seleccionada.  
  
3.  Suelte el botón del mouse (ratón). Aparecerá el cuadro de diálogo **Tablas y columnas** .  
  
4.  Seleccione la columna de clave externa y la tabla y columna de clave principal con las desea establecer una relación.  
  
5.  Elija **Aceptar** dos veces para crear la relación.  
  
 Cuando ejecute consultas en una tabla, puede utilizar una relación reflexiva para crear una autocombinación. Para más información sobre cómo consultar las tablas con combinaciones, consulte [Realizar consultas con combinaciones &#40;Visual Database Tools&#41;](visual-database-tools.md).  
  
## <a name="see-also"></a>Vea también  
 [Realizar consultas con combinaciones &#40;Visual Database Tools&#41;](visual-database-tools.md)  
  
  
