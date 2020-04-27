---
title: Crear relaciones entre tablas en un diagrama (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- diagrams [SQL Server], designing
ms.assetid: 28e9630c-dff4-46cc-bb0e-fe77998b6ac2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ab36ebfefbfd3d8cee8e6da7caadf86eb4a10032
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63184279"
---
# <a name="create-relationships-between-tables-on-a-diagram-visual-database-tools"></a>Crear relaciones entre tablas en un diagrama (Visual Database Tools)
  Puede crear relaciones entre columnas de diferentes tablas en el Diseñador de diagramas si se arrastran las columnas entre las tablas.  
  
### <a name="to-create-a-relationship-graphically"></a>Para crear una relación gráficamente  
  
1.  En el Diseñador de bases de datos, haga clic en el selector de fila de una o varias columnas de la base de datos que desea poner en relacionar con una columna de otra tabla.  
  
2.  Arrastre las columnas seleccionadas hasta la tabla relacionada.  
  
3.  Aparecen dos cuadros de diálogo: **Relación de clave externa** y **Tablas y columnas**, esta última en primer plano.  
  
4.  **Nombre de la relación** incluye un nombre proporcionado por el sistema con el formato FK_*tablalocal*_*tablaexterna*. Se puede modificar este valor.  
  
5.  Compruebe que **Tabla de clave principal** especifica la tabla correcta.  
  
6.  En la cuadrícula se enumeran las columnas locales y las columnas externas coincidentes. Puede agregar o quitar columnas de la tabla, así como modificar las asignaciones.  
  
7.  Elija **Aceptar**.  
  
     Aparecerá el cuadro de diálogo **Relación de clave externa** . **Relación seleccionada** muestra la relación que haya creado.  
  
8.  Cambie las propiedades de la relación en la cuadrícula.  
  
9. Elija **Aceptar** para crear la relación.  
  
     El Diseñador de bases de datos muestra una relación entre las columnas que haya elegido.  
  
## <a name="see-also"></a>Consulte también  
 [Cuadro de diálogo tablas y columnas &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Restricciones UNIQUE y restricciones check](../../relational-databases/tables/unique-constraints-and-check-constraints.md)   
 [Trabajar con tablas en diagramas de base de datos &#40;Visual Database Tools&#41;](work-with-tables-in-database-diagram-visual-database-tools.md)  
  
  
