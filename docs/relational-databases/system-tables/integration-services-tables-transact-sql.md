---
title: Tablas (Transact-SQL) de Integration Services | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- SQL Server Integration Services system tables
- system tables [SQL Server], Integration Services
- system tables [Integration Services]
- SSIS, system tables
ms.assetid: 683b181b-0091-4a9c-86db-bc577af43cec
caps.latest.revision: 21
author: douglasl
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fc5df46211b3de92b054fea4120d9b7c884a0ccb
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33259625"
---
# <a name="integration-services-tables-transact-sql"></a>Tablas de Integration Services (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  En los temas de esta sección se describen las tablas del sistema de la base de datos msdb que almacenan información usada por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
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
  
  
