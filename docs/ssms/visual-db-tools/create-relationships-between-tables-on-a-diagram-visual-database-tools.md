---
title: Crear relaciones entre tablas en un diagrama | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- diagrams [SQL Server], designing
ms.assetid: 28e9630c-dff4-46cc-bb0e-fe77998b6ac2
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: a6722dcbc9f9052803ef32a3b1bdb75a9e06de31
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2019
ms.locfileid: "65090021"
---
# <a name="create-relationships-between-tables-on-a-diagram-visual-database-tools"></a>Crear relaciones entre tablas en un diagrama (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Puede crear relaciones entre columnas de diferentes tablas en el Diseñador de diagramas si se arrastran las columnas entre las tablas.  
  
### <a name="to-create-a-relationship-graphically"></a>Para crear una relación gráficamente  
  
1.  En el Diseñador de bases de datos, haga clic en el selector de fila de una o varias columnas de la base de datos que desea poner en relacionar con una columna de otra tabla.  
  
2.  Arrastre las columnas seleccionadas hasta la tabla relacionada.  
  
3.  Aparecen dos cuadros de diálogo: **Relación de clave externa** y **Tablas y columnas**, esta última en primer plano.  
  
4.  **Nombre de la relación** incluye un nombre proporcionado por el sistema con el formato FK_*tablalocal*\_*tablaexterna*. Se puede modificar este valor.  
  
5.  Compruebe que **Tabla de clave principal** especifica la tabla correcta.  
  
6.  En la cuadrícula se enumeran las columnas locales y las columnas externas coincidentes. Puede agregar o quitar columnas de la tabla, así como modificar las asignaciones.  
  
7.  Elija **Aceptar**.  
  
    Aparecerá el cuadro de diálogo **Relación de clave externa** . **Relación seleccionada** muestra la relación que haya creado.  
  
8.  Cambie las propiedades de la relación en la cuadrícula.  
  
9. Elija **Aceptar** para crear la relación.  
  
    El Diseñador de bases de datos muestra una relación entre las columnas que haya elegido.  
  
## <a name="see-also"></a>Consulte también  
[Cuadro de diálogo Tablas y columnas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/tables-and-columns-dialog-box-visual-database-tools.md)  
[Trabajar con restricciones (Visual Database Tools)](https://msdn.microsoft.com/637098af-2567-48f8-90f4-b41df059833e)  
[Trabajar con tablas en diagramas de base de datos &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-tables-in-database-diagram-visual-database-tools.md)  
  
