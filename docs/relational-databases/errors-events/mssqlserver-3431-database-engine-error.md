---
title: MSSQLSERVER_3431 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3431 (Database Engine error)
ms.assetid: 9541217f-e5c6-4a12-a19a-006058f1d3f3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 921dde33b466cf9f72a8254f304d2a0abd739f7e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68132389"
---
# <a name="mssqlserver_3431"></a>MSSQLSERVER_3431
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|3431|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|UNRESOLVED_XACT|  
|Texto del mensaje|No se pudo recuperar la base de datos '%.*ls' (id. %d) debido a resultados de transacciones sin resolver. Se prepararon transacciones del Microsoft DTC (Coordinador de transacciones distribuidas), pero Microsoft DTC no pudo determinar la resolución. Para solucionar este problema, corrija MS DTC, realice una restauración a partir de una copia de seguridad completa o repare la base de datos.|  
  
## <a name="explanation"></a>Explicación  
Una o más transacciones distribuidas que estaban usando el Coordinador de transacciones distribuidas de [!INCLUDE[msCoName](../../includes/msconame-md.md)] (MS DTC) estaban incompletas cuando se cerró la base de datos. Se originó un error al recuperar esta base de datos debido a que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede completar o revertir las transacciones sin más información de MS DTC.  
  
## <a name="user-action"></a>Acción del usuario  
Para recuperar esta base de datos, primero debe resolver el problema con MS DTC. Para estudiar el problema con MS DTC, examine los registros de eventos de Windows. Si no puede resolver el problema con MS DTC y recuperar la base de datos, restaure una copia de seguridad de la base de datos.  
  
