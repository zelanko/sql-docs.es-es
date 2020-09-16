---
description: Agregar tabla (cuadro de diálogo, Visual Database Tools)
title: Cuadro de diálogo Agregar tabla (Diseñador de bases de datos)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:65555
- vdt.dlgbox.schema.addtable
ms.assetid: 3c0b1b30-795c-4240-91d6-890b8348014a
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: 53898206b1111119dad7056e420bf7395d326007
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497341"
---
# <a name="add-table-dialog-box-database-designer-visual-database-tools"></a>Agregar tabla (cuadro de diálogo, Visual Database Tools)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Permite agregar tablas en el Diseñador de bases de datos.  
  
> [!NOTE]  
> Si se publica la tabla para la replicación, debe modificar el esquema mediante la instrucción Transact-SQL [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) u Objetos de administración de SQL Server (SMO). Si se modifica el esquema mediante el Diseñador de tablas o el Diseñador de diagramas de base de datos, se intentará eliminar la tabla y volver a crearla. No se pueden eliminar objetos publicados, por lo que la modificación del esquema generará un error.  
  
## <a name="ui-element-list"></a>Lista de elementos de la interfaz de usuario  
**Actualizar**  
Actualiza la lista de tablas para que coincidan con el estado actual de la base de datos.  
  
**Add (Agregar)**  
Agrega las tablas seleccionadas.  
  
> [!NOTE]  
> Si desea agregar varias tablas al diagrama, puede seleccionarlas todas antes de hacer clic en **Agregar**. Como alternativa, puede hacer doble clic en cada una de las tablas que desee agregar y, luego, hacer clic en **Cerrar** cuando termine.  
  
**Close**  
Cierra el cuadro de diálogo sin agregar más tablas.  
  
## <a name="see-also"></a>Consulte también  
[Agregar tablas a diagramas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-tables-to-diagrams-visual-database-tools.md)  
  
