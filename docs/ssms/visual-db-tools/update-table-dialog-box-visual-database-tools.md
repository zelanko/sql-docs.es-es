---
title: Cuadro de diálogo Actualizar tabla
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.updatetable
- vdtsql.chm:69643
ms.assetid: 174c7275-5b15-42a9-b172-5ff30de575a1
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: 5af6b442486a1c80a1b9ec9f8d870f167c67de35
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "75246040"
---
# <a name="update-table-dialog-box-visual-database-tools"></a>Actualizar tabla (cuadro de diálogo, Visual Database Tools)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Este cuadro de diálogo permite especificar la tabla que se va a actualizar.

Este cuadro de diálogo aparece si se muestran varias tablas en el panel Diagrama cuando cambia una consulta al tipo Update.  

Seleccione la tabla que desea actualizar y, luego, elija **Aceptar**.

> [!NOTE]
> Si se publica la tabla para la replicación, debe modificar el esquema mediante la instrucción Transact-SQL [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) u Objetos de administración de SQL Server (SMO). Si se modifica el esquema mediante el Diseñador de tablas o el Diseñador de diagramas de base de datos, se intentará eliminar la tabla y volver a crearla. No se pueden eliminar objetos publicados, por lo que la modificación del esquema generará un error.

## <a name="see-also"></a>Consulte también

[Crear consultas de actualización](../../ssms/visual-db-tools/create-update-queries-visual-database-tools.md)