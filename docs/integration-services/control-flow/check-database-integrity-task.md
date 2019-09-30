---
title: Tarea Comprobar la integridad de la base de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.checkdatabaseintegritytask.f1
helpviewer_keywords:
- data integrity [Integration Services]
- Check Database Integrity task [Integration Services]
- checking database consistency
- database consistency checks [Integration Services]
- verifying database consistency
- integrity checking [Integration Services]
ms.assetid: 5a82fe99-4503-429f-9337-e6bac7649fe4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 676bbf9fb96521ceaa24f58b448182506307f691
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298397"
---
# <a name="check-database-integrity-task"></a>Tarea Comprobar la integridad de la base de datos

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La tarea Comprobar la integridad de la base de datos comprueba la asignación y la integridad estructural de todos los objetos de la base de datos especificada. Esta tarea puede comprobar una o varias bases de datos, y se puede elegir comprobar también los índices de las bases de datos.  
  
 Esta tarea encapsula la instrucción DBCC CHECKDB. Para obtener más información, vea [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md).  
  
## <a name="configuration-of-the-check-database-integrity-task"></a>Configuración de la tarea Comprobar la integridad de la base de datos  
 Puede establecer propiedades a través del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Esta tarea se encuentra en la sección **Tareas del plan de mantenimiento** del **Cuadro de herramientas** , en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
-   [Tarea Comprobar la integridad de la base de datos &#40;Plan de mantenimiento&#41;](../../relational-databases/maintenance-plans/check-database-integrity-task-maintenance-plan.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
  
