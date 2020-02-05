---
title: MSSQLSERVER_5231 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5231 (Database Engine error)
ms.assetid: 6954ae84-ed0b-4f4c-9d0a-e73f3d71476c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2cd4a8208925f6e0fe0a0fed4b162b4eb7361009
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68122961"
---
# <a name="mssqlserver_5231"></a>MSSQLSERVER_5231
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|5231|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC4_DEADLOCK_SKIPPED_OBJECT|  
|Texto del mensaje|Id. de objeto O_ID (objeto 'NAME'): Se ha producido un interbloqueo al intentar bloquear este objeto para la comprobación. Este objeto ha sido omitido y no se va a procesar.|  
  
## <a name="explanation"></a>Explicación  
Se ha producido un interbloqueo cuando DBCC intentaba bloquear el objeto; DBCC ha sido elegido como víctima del interbloqueo. El objeto no se procesará.  
  
## <a name="user-action"></a>Acción del usuario  
None  
  
