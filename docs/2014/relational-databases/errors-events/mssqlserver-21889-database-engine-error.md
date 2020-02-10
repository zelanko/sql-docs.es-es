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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62915232"
---
# <a name="mssqlserver_21889"></a>MSSQLSERVER_21889
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|21889|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQLErrorNum21889|  
|Texto del mensaje|La instancia '%s' de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no es un publicador de replicación. Ejecute `sp_adddistributor` en la instancia '%s' de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el distribuidor '%s' a fin de habilitar la instancia para hospedar la base de datos de publicación '%s'. Asegúrese de especificar el mismo inicio de sesión y contraseña que se usarán para el publicador original.|  
  
## <a name="explanation"></a>Explicación  
 Para hospedar la base de datos del publicador, la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser un publicador de replicación. 
  `sp_validate_redirected_publisher` llama a `sp_helpdistributor` en el servidor remoto para determinar si el servidor es un publicador de replicación. Se devuelve este error cuando la ejecución del procedimiento almacenado `sp_helpdistributor` indica que la instancia de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no es un publicador de replicación.  
  
## <a name="user-action"></a>Acción del usuario  
 Ejecute `sp_adddistributor` en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda la base de datos del publicador. Al ejecutar `sp_adddistributor`, especifique el distribuidor correcto. Use el mismo valor para el *@password* parámetro que el que se `sp_adddistributor` utilizó cuando se ejecutó inicialmente en el distribuidor.  
  
  
