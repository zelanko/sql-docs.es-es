---
title: Organizar trabajos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- job category
- organize jobs
ms.assetid: 629c3e06-f933-483b-8621-280dbb7a7bd1
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 844b71d9f24e5f4c9ddf28d308cdea1b9d3b6bfb
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2018
---
# <a name="organize-jobs"></a>organizar los trabajos
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

Las categorías de trabajo le ayudan a organizar los trabajos para poder filtrarlos y agruparlos fácilmente. Por ejemplo, puede organizar todos los trabajos de copia de seguridad de las bases de datos en la categoría Mantenimiento de bases de datos. También puede crear sus propias categorías.  
  
> [!WARNING]  
> Las categorías multiservidor existen solo en los servidores maestros. Solo hay una categoría de trabajo predeterminada disponible en un servidor maestro: [**Sin categoría (Multiservidor)**]. Cuando se descarga un trabajo multiservidor, su categoría se cambia a **Trabajos del servidor principal** en el servidor de destino.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Descripción**|**Tema**|  
|Describe cómo crear una categoría de trabajo.|[Crear una categoría de trabajo](../../ssms/agent/create-a-job-category.md)|  
|Describe cómo eliminar una categoría de trabajo.|[Eliminar una categoría de trabajo](../../ssms/agent/delete-a-job-category.md)|  
|Describe cómo asignar un trabajo a una categoría de trabajo.|[Asignar un trabajo a una categoría de trabajo](../../ssms/agent/assign-a-job-to-a-job-category.md)|  
|Describe cómo cambiar la pertenencia a una categoría de trabajo.|[Change the Membership of a Job Category](../../ssms/agent/change-the-membership-of-a-job-category.md)|  
|Describe cómo mostrar información de categorías.|[Mostrar información de categorías de trabajo](../../ssms/agent/list-job-category-information.md)|  
  
