---
title: MSSQLSERVER_21889 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 21889 (Database Engine error)
ms.assetid: ae199540-7986-4cc2-b782-cd22793236d3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 262b2c795da92b2ef32c6956d9a2deda0e45a39d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48151925"
---
# <a name="mssqlserver21889"></a>MSSQLSERVER_21889
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|21889|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQLErrorNum21889|  
|Texto del mensaje|La instancia '%s' de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no es un publicador de replicación. Ejecute `sp_adddistributor` en la instancia '%s' de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el distribuidor '%s' a fin de habilitar la instancia para hospedar la base de datos de publicación '%s'. Asegúrese de especificar el mismo inicio de sesión y contraseña que se usarán para el publicador original.|  
  
## <a name="explanation"></a>Explicación  
 Para hospedar la base de datos del publicador, la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser un publicador de replicación. `sp_validate_redirected_publisher` llama a `sp_helpdistributor` en el servidor remoto para determinar si el servidor es un publicador de replicación. Se devuelve este error cuando la ejecución del procedimiento almacenado `sp_helpdistributor` indica que la instancia de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no es un publicador de replicación.  
  
## <a name="user-action"></a>Acción del usuario  
 Ejecute `sp_adddistributor` en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda la base de datos del publicador. Al ejecutar `sp_adddistributor`, especifique el distribuidor correcto. Use el mismo valor para el *@password* parámetro que usa cuando `sp_adddistributor` se ejecutó inicialmente en el distribuidor.  
  
  
