---
title: "Cuadro de diálogo Agregar tabla (Diseñador de bases de datos) (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdtsql.chm:65555
- vdt.dlgbox.schema.addtable
ms.assetid: 3c0b1b30-795c-4240-91d6-890b8348014a
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a13a8f643a66c8357f17af11a00f47bd7ec3b5a1
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2018
---
# <a name="add-table-dialog-box-database-designer-visual-database-tools"></a>Agregar tabla (cuadro de diálogo, Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Permite agregar tablas en el Diseñador de bases de datos.  
  
> [!NOTE]  
> Si se publica la tabla para la replicación, debe modificar el esquema mediante la instrucción Transact-SQL [ALTER TABLE](http://msdn.microsoft.com/en-us/f1745145-182d-4301-a334-18f799d361d1) u Objetos de administración de SQL Server (SMO). Si se modifica el esquema mediante el Diseñador de tablas o el Diseñador de diagramas de base de datos, se intentará eliminar la tabla y volver a crearla. No se pueden eliminar objetos publicados, por lo que la modificación del esquema generará un error.  
  
## <a name="uielement-list"></a>Lista de UIElement  
**Actualizar**  
Actualiza la lista de tablas para que coincidan con el estado actual de la base de datos.  
  
**Agregar**  
Agrega las tablas seleccionadas.  
  
> [!NOTE]  
> Si desea agregar varias tablas al diagrama, puede seleccionarlas todas antes de hacer clic en **Agregar**. Como alternativa, puede hacer doble clic en cada una de las tablas que desee agregar y, luego, hacer clic en **Cerrar** cuando termine.  
  
**Cerrar**  
Cierra el cuadro de diálogo sin agregar más tablas.  
  
## <a name="see-also"></a>Ver también  
[Agregar tablas a diagramas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-tables-to-diagrams-visual-database-tools.md)  
  
