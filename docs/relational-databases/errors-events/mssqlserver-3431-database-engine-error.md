---
title: MSSQLSERVER_3431 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 3431 (Database Engine error)
ms.assetid: 9541217f-e5c6-4a12-a19a-006058f1d3f3
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e7f4faa34293cba8f9b14e8b4d4b2c998f1eb12e
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver3431"></a>MSSQLSERVER_3431
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|3431|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|UNRESOLVED_XACT|  
|Texto del mensaje|No se pudo recuperar la base de datos '%.*ls' (id. %d) debido a resultados de transacciones sin resolver. Se prepararon transacciones del Microsoft DTC (Coordinador de transacciones distribuidas), pero Microsoft DTC no pudo determinar la resolución. Para solucionar este problema, corrija MS DTC, realice una restauración a partir de una copia de seguridad completa o repare la base de datos.|  
  
## <a name="explanation"></a>Explicación  
Una o más transacciones distribuidas que estaban usando el Coordinador de transacciones distribuidas de [!INCLUDE[msCoName](../../includes/msconame-md.md)] (MS DTC) estaban incompletas cuando se cerró la base de datos. Se originó un error al recuperar esta base de datos debido a que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede completar o revertir las transacciones sin más información de MS DTC.  
  
## <a name="user-action"></a>Acción del usuario  
Para recuperar esta base de datos, primero debe resolver el problema con MS DTC. Para estudiar el problema con MS DTC, examine los registros de eventos de Windows. Si no puede resolver el problema con MS DTC y recuperar la base de datos, restaure una copia de seguridad de la base de datos.  
  

