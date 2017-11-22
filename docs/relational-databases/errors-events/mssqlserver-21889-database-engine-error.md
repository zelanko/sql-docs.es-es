---
title: MSSQLSERVER_21889 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 21889 (Database Engine error)
ms.assetid: ae199540-7986-4cc2-b782-cd22793236d3
caps.latest.revision: "6"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 44c79bc99f26399ec6494deb249342ce3037123a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver21889"></a>MSSQLSERVER_21889
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|21889|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQLErrorNum21889|  
|Texto del mensaje|La instancia '%s' de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no es un publicador de replicación. Ejecute **sp_adddistributor** en la instancia '%s' de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el distribuidor '%s' a fin de habilitar la instancia para hospedar la base de datos de publicación '%s'. Asegúrese de especificar el mismo inicio de sesión y contraseña que se usarán para el publicador original.|  
  
## <a name="explanation"></a>Explicación  
Para hospedar la base de datos del publicador, la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser un publicador de replicación. **sp_validate_redirected_publisher** llama a **sp_helpdistributor** en el servidor remoto para determinar si el servidor es un publicador de replicación. Se devuelve este error cuando la ejecución del procedimiento almacenado **sp_helpdistributor** indica que la instancia de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no es un publicador de replicación.  
  
## <a name="user-action"></a>Acción del usuario  
Ejecute **sp_adddistributor** en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda la base de datos del publicador. Al ejecutar **sp_adddistributor**, especifique el distribuidor correcto. Use el mismo valor para el parámetro *@password* que se usó cuando se ejecutó **sp_adddistributor** inicialmente en el distribuidor.  
  
