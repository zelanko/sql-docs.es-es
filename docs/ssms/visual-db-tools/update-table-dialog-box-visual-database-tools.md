---
title: Cuadro de diálogo Actualizar tabla (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.updatetable
- vdtsql.chm:69643
ms.assetid: 174c7275-5b15-42a9-b172-5ff30de575a1
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: ef55e7c73bf9aec256a2ec2d89a4734fe40b18a3
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2019
ms.locfileid: "65098528"
---
# <a name="update-table-dialog-box-visual-database-tools"></a>Actualizar tabla (cuadro de diálogo, Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Este cuadro de diálogo permite especificar la tabla que se va a actualizar.  
  
Este cuadro de diálogo aparece si se muestran varias tablas en el panel Diagrama cuando cambia una consulta al tipo Update.  
  
Seleccione la tabla que desea actualizar y, luego, elija **Aceptar**.  
  
> [!NOTE]  
> Si se publica la tabla para la replicación, debe modificar el esquema mediante la instrucción Transact-SQL [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) u Objetos de administración de SQL Server (SMO). Si se modifica el esquema mediante el Diseñador de tablas o el Diseñador de diagramas de base de datos, se intentará eliminar la tabla y volver a crearla. No se pueden eliminar objetos publicados, por lo que la modificación del esquema generará un error.  
  
## <a name="see-also"></a>Consulte también  
[Crear consultas de actualización (Visual Database Tools)](../../ssms/visual-db-tools/create-update-queries-visual-database-tools.md)  
  
