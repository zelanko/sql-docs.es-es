---
title: Cuadro de diálogo operaciones activas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.isoperations.executions.f1
- sql12.ssis.ssms.isoperations.general.f1
ms.assetid: 5bb0fcd6-0ce9-488a-85b8-25dddaa03cda
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f930a2e6f3ce84c330a4b7292ebaaba3b2ab871e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062218"
---
# <a name="active-operations-dialog-box"></a>Operaciones activas, cuadro de diálogo
  Utilice el cuadro de diálogo **Operaciones activas** para ver el estado de las operaciones de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que se están ejecutando actualmente en el servidor de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , como implementación, validación, y ejecución del paquete. Estos datos se almacenan en el catálogo de SSISDB.  
  
 Para obtener más información sobre las vistas de [!INCLUDE[tsql](../includes/tsql-md.md)] relacionadas, vea [catalog.operations &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-operations-ssisdb-database), [catalog.validations &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-validations-ssisdb-database) y [catalog.executions &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-executions-ssisdb-database).  
  
 **¿Qué desea hacer?**  
  
1.  [Abrir el cuadro de diálogo Operaciones activas](#open_dialog)  
  
2.  [Configurar las opciones](#options)  
  
##  <a name="open_dialog"></a> Abrir el cuadro de diálogo Operaciones activas  
  
1.  Abra [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
  
2.  Conéctese al motor de base de datos de Microsoft SQL Server  
  
3.  En el Explorador de objetos, expanda el nodo **Integration Services** , haga clic con el botón derecho en **SSISDB**y, después, haga clic en **Operaciones activas**.  
  
##  <a name="options"></a> Configurar las opciones  
  
### <a name="options"></a>Opciones  
 **Tipo**  
 Especifica el tipo de operación. Los siguientes son los valores posibles para el **tipo** campo y los valores correspondientes en la columna operations_type de la instrucción Transact-SQL `catalog.operations` vista.  
  
|||  
|-|-|  
|Inicialización de Integration Services|1|  
|Limpieza de operaciones (trabajo del Agente SQL Server)|2|  
|Limpieza de versiones de proyecto (trabajo del Agente SQL Server)|3|  
|Implementar proyecto|101|  
|Restaurar proyecto|106|  
|Crear e iniciar la ejecución del paquete|200|  
|Detener operación (detención de una validación o una ejecución)|202|  
|Validar proyecto|300|  
|Validar paquete|301|  
|Configurar catálogo|1000|  
  
 **Detener**  
 Haga clic para detener una operación que se esté ejecutando actualmente.  
  
  
