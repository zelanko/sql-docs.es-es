---
description: Propiedades del trabajo - Nuevo trabajo (página Programaciones)
title: Propiedades del trabajo - Nuevo trabajo (página Programaciones)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.schedules.f1
ms.assetid: 0b03585b-a510-484d-8a63-9b32459def9c
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c4476f26f2b17cedcc12e723efc08c116b190488
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037893"
---
# <a name="job-properties---new-job-schedules-page"></a>Propiedades del trabajo - Nuevo trabajo (página Programaciones)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance), actualmente son compatibles la mayoría de las características del Agente SQL Server. Consulte [Diferencias entre T-SQL de Azure SQL Managed Instance y SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para más información.

Use esta página para ver y organizar las programaciones de un trabajo del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="options"></a>Opciones  
**Lista de programaciones**  
Muestra las programaciones para este trabajo.  
  
**Nuevo**  
Crea una nueva programación. Una vez que se haya creado la programación, ésta se agregará al trabajo.  
  
**Seleccionar**  
Selecciona una de las programaciones existentes. Puesto que un trabajo y una programación deben tener el mismo propietario, esta opción solo le permitirá seleccionar programaciones de su propiedad.  
  
**Edición**  
Edita la programación seleccionada para cambiar las propiedades de programación del trabajo.  
  
**Remove**  
Quita la programación seleccionada del trabajo. Si no hay otros trabajos que utilicen la programación, ésta se elimina de la base de datos.  
  
## <a name="see-also"></a>Consulte también  
[Implementar trabajos](../../ssms/agent/implement-jobs.md)  
