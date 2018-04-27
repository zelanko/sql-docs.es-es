---
title: Crear relaciones entre tablas en un diagrama | Microsoft Docs
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
- diagrams [SQL Server], designing
ms.assetid: 28e9630c-dff4-46cc-bb0e-fe77998b6ac2
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1c2a47c9aea56a731dc9b214ba6dc07de569c3dc
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="create-relationships-between-tables-on-a-diagram-visual-database-tools"></a>Crear relaciones entre tablas en un diagrama (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
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
  
## <a name="see-also"></a>Ver también  
[Cuadro de diálogo Tablas y columnas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/tables-and-columns-dialog-box-visual-database-tools.md)  
[Trabajar con restricciones (Visual Database Tools)](http://msdn.microsoft.com/en-us/637098af-2567-48f8-90f4-b41df059833e)  
[Trabajar con tablas en diagramas de base de datos &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-tables-in-database-diagram-visual-database-tools.md)  
  
