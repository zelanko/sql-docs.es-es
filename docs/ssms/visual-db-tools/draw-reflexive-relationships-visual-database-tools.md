---
title: Dibujar relaciones reflexivas (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- drawing reflexive relationships
- reflexive relationships
- database diagrams [SQL Server], relationships
ms.assetid: e218363f-faec-46d5-9904-a537fbcc994d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: be3abc83b3084626f714efa6628fc7cfe1547867
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105309"
---
# <a name="draw-reflexive-relationships-visual-database-tools"></a>Dibujar relaciones reflexivas (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Puede crear una relación reflexiva para vincular una o más columnas de una tabla con una o más columnas de la misma tabla. Por ejemplo, suponga que la tabla `employee` contiene una columna `emp_id` y una columna `mgr_id` . Como cada director también es un empleado, para relacionar estas dos columnas debe dibujar una línea de relación desde la tabla hasta la propia tabla. Esta relación garantiza que cada Id. de director que se agregue a la tabla coincida con un Id. de empleado existente.  
  
Antes de crear una relación debe definir una restricción PRIMARY KEY o UNIQUE para la tabla. Después debe relacionar la columna de clave principal con una columna coincidente. Cuando haya creado la relación, la columna coincidente se convertirá en una clave externa de la tabla.  
  
### <a name="to-draw-a-reflexive-relationship"></a>Para dibujar una relación reflexiva  
  
1.  En el diagrama de base de datos, haga clic en el selector de fila de la columna de base de datos que desea relacionar con otra columna y arrastre el puntero fuera de la tabla hasta que aparezca una línea.  
  
2.  Arrastre la línea hasta la tabla seleccionada.  
  
3.  Suelte el botón del mouse (ratón). Aparecerá el cuadro de diálogo **Tablas y columnas** .  
  
4.  Seleccione la columna de clave externa y la tabla y columna de clave principal con las desea establecer una relación.  
  
5.  Elija **Aceptar** dos veces para crear la relación.  
  
Cuando ejecute consultas en una tabla, puede utilizar una relación reflexiva para crear una autocombinación. Para más información sobre cómo consultar las tablas con combinaciones, consulte [Realizar consultas con combinaciones &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md).  
  
## <a name="see-also"></a>Consulte también  
[Realizar consultas con combinaciones &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
