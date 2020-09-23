---
description: organizar los trabajos
title: organizar los trabajos
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- job category
- organize jobs
ms.assetid: 629c3e06-f933-483b-8621-280dbb7a7bd1
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ad737fea7ae2a9c55977ffb9d838fdcbeccad412
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88319051"
---
# <a name="organize-jobs"></a>organizar los trabajos
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Azure SQL Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), actualmente son compatibles la mayoría de las características del Agente SQL Server. Consulte [Diferencias entre T-SQL de Azure SQL Managed Instance y SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para más información.

Las categorías de trabajo le ayudan a organizar los trabajos para poder filtrarlos y agruparlos fácilmente. Por ejemplo, puede organizar todos los trabajos de copia de seguridad de las bases de datos en la categoría Mantenimiento de bases de datos. También puede crear sus propias categorías.  
  
> [!WARNING]  
> Las categorías multiservidor existen solo en los servidores maestros. Solo hay una categoría de trabajo predeterminada disponible en un servidor maestro: [**Sin categoría (Multiservidor)**]. Cuando se descarga un trabajo multiservidor, su categoría se cambia a **Trabajos del servidor principal** en el servidor de destino.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción|Tema|  
|-|-|  
|Describe cómo crear una categoría de trabajo.|[Crear una categoría de trabajo](../../ssms/agent/create-a-job-category.md)|  
|Describe cómo eliminar una categoría de trabajo.|[Eliminar una categoría de trabajo](../../ssms/agent/delete-a-job-category.md)|  
|Describe cómo asignar un trabajo a una categoría de trabajo.|[Asignar un trabajo a una categoría de trabajo](../../ssms/agent/assign-a-job-to-a-job-category.md)|  
|Describe cómo cambiar la pertenencia a una categoría de trabajo.|[Change the Membership of a Job Category](../../ssms/agent/change-the-membership-of-a-job-category.md)|  
|Describe cómo mostrar información de categorías.|[Mostrar información de categorías de trabajo](../../ssms/agent/list-job-category-information.md)|  
  
