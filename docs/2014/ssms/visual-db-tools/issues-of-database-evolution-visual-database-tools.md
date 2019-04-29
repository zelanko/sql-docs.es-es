---
title: Problemas de evolución de bases de datos (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], multuser database changes
- database evolution [SQL Server]
ms.assetid: 1ed6ae10-d212-4ec2-8569-1b94ab1cba6d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d3a1f10ae77061983a5cf64ddd5a3462bb4be49b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63035594"
---
# <a name="issues-of-database-evolution-visual-database-tools"></a>Problemas de evolución de bases de datos (Visual Database Tools)
  Si cambia la estructura de una base de datos implementada, debe tener especial cuidado para que la modificación sea compatible con la estructura de la base de datos y los datos existentes. Es posible que tenga que seguir pasos especiales cuando realice las modificaciones siguientes:  
  
-   **Agregar una restricción** Si agrega una restricción, es posible que la base de datos ya contenga datos que no la satisfagan. Cuando intente guardar la restricción nueva, el [cuadro de diálogo Notificaciones después de guardar &#40;Visual Database Tools&#41;](visual-database-tools.md) le informará que el servidor de base de datos no pudo crear la restricción. Para forzar a la base de datos a aceptar la restricción nueva, puede desactivar la casilla **Comprobar datos existentes al crear**.  
  
-   **Agregar una relación** Si agrega una relación, es posible que la base de datos ya contenga filas de la tabla de clave externa sin filas correspondientes en la tabla de clave principal. Es decir, es posible que los datos existentes no satisfagan la integridad referencial. Cuando intente guardar la relación nueva, el [cuadro de diálogo Notificaciones después de guardar &#40;Visual Database Tools&#41;](visual-database-tools.md) le informará que el servidor de base de datos no pudo guardar la tabla de clave externa revisada. Para forzar a la base de datos a aceptar la modificación, puede desactivar la casilla **Comprobar datos existentes al crear**.  
  
-   **Modificar una tabla que contribuye a una vista indizada** Si modifica una tabla que contribuye a una vista indizada de Microsoft SQL Server, se perderán los índices de la vista. Vea los Libros en pantalla de SQL Server para obtener información sobre cómo volver a crear ííndices.  
  
-   **Eliminar un objeto** Si elimina un objeto, como una columna, una tabla o una vista, primero asegúrese de no hay ningún otro objeto en la base de datos que contenga una referencia a ese objeto.  
  
 Independientemente de la manera en que se modifique el diseño de base de datos, debe conservar un historial de las modificaciones. Una posibilidad es conservar scripts SQL para todas las modificaciones que haya realizado en la base de datos de producción.  
  
## <a name="see-also"></a>Vea también  
 [Restricciones UNIQUE y restricciones Check](../../relational-databases/tables/unique-constraints-and-check-constraints.md)   
 [Entornos multiusuario &#40;Visual Database Tools&#41;](multiuser-environments-visual-database-tools.md)  
  
  
