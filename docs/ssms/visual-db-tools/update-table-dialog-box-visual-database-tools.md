---
title: "Cuadro de diálogo Actualizar tabla (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdt.dlgbox.updatetable
- vdtsql.chm:69643
ms.assetid: 174c7275-5b15-42a9-b172-5ff30de575a1
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e0abd8866fecfd845e56cd1ea26eabfc87b1e3b5
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="update-table-dialog-box-visual-database-tools"></a>Actualizar tabla (cuadro de diálogo, Visual Database Tools)
Este cuadro de diálogo permite especificar la tabla que se va a actualizar.  
  
Este cuadro de diálogo aparece si se muestran varias tablas en el panel Diagrama cuando cambia una consulta al tipo Update.  
  
Seleccione la tabla que desea actualizar y, luego, elija **Aceptar**.  
  
> [!NOTE]  
> Si se publica la tabla para la replicación, debe modificar el esquema mediante la instrucción Transact-SQL [ALTER TABLE](http://msdn.microsoft.com/en-us/f1745145-182d-4301-a334-18f799d361d1) u Objetos de administración de SQL Server (SMO). Si se modifica el esquema mediante el Diseñador de tablas o el Diseñador de diagramas de base de datos, se intentará eliminar la tabla y volver a crearla. No se pueden eliminar objetos publicados, por lo que la modificación del esquema generará un error.  
  
## <a name="see-also"></a>Vea también  
[Crear consultas de actualización (Visual Database Tools)](../../ssms/visual-db-tools/create-update-queries-visual-database-tools.md)  
  

