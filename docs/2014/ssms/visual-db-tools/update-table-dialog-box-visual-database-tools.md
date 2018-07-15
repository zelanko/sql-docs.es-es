---
title: Cuadro de diálogo Actualizar tabla (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.updatetable
- vdtsql.chm:69643
ms.assetid: 174c7275-5b15-42a9-b172-5ff30de575a1
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 888cc051f9df04982825c10ebdb83ec614d78389
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37257641"
---
# <a name="update-table-dialog-box-visual-database-tools"></a>Actualizar tabla (cuadro de diálogo, Visual Database Tools)
  Este cuadro de diálogo permite especificar la tabla que se va a actualizar.  
  
 Este cuadro de diálogo aparece si se muestran varias tablas en el panel Diagrama cuando cambia una consulta al tipo Update.  
  
 Seleccione la tabla que desea actualizar y, luego, elija **Aceptar**.  
  
> [!NOTE]  
>  Si se publica la tabla para la replicación, debe modificar el esquema mediante la instrucción Transact-SQL [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) u Objetos de administración de SQL Server (SMO). Si se modifica el esquema mediante el Diseñador de tablas o el Diseñador de diagramas de base de datos, se intentará eliminar la tabla y volver a crearla. No se pueden eliminar objetos publicados, por lo que la modificación del esquema generará un error.  
  
## <a name="see-also"></a>Vea también  
 [Crear consultas de actualización &#40;Visual Database Tools&#41;](visual-database-tools.md)  
  
  
