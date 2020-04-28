---
title: Tablas de Integration Services (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- SQL Server Integration Services system tables
- system tables [SQL Server], Integration Services
- system tables [Integration Services]
- SSIS, system tables
ms.assetid: 683b181b-0091-4a9c-86db-bc577af43cec
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 61379adc04eddaf276fae37879674b63833b76e7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67990135"
---
# <a name="integration-services-tables-transact-sql"></a>Tablas de Integration Services (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  En los temas de esta sección se describen las tablas del sistema de la base de datos msdb [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]que almacenan información utilizada por.  
  
## <a name="in-this-section"></a>En esta sección  
 [sysssislog](../../relational-databases/system-tables/sysssislog-transact-sql.md)  
 Contiene una fila para cada entrada del registro que un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] genera en tiempo de ejecución.  
  
 Esta tabla solo se utiliza cuando los paquetes utilizan el proveedor de registro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [sysssispackagefolders](../../relational-databases/system-tables/sysssispackagefolders-transact-sql.md)  
 Contiene una fila para cada carpeta lógica que el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa para organizar paquetes. Los valores de columna definen las relaciones primario-secundario entre carpetas anidadas.  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] muestra los paquetes almacenados en una vista jerárquica cuando se establece conexión con el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [sysssispackages](../../relational-databases/system-tables/sysssispackages-transact-sql.md)  
 Contiene una fila para cada paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Esta tabla solo se utiliza cuando se almacenan paquetes en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
