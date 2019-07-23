---
title: MSSQLSERVER_3452 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3452 (Database Engine error)
ms.assetid: bf838f02-7186-4b33-b01e-361b0c02de1f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a11f78e1ef38e432ba2b999877e6e5384ac1f386
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68043657"
---
# <a name="mssqlserver3452"></a>MSSQLSERVER_3452
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|3452|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|REC_CHECKIDENTITY|  
|Texto del mensaje|En la recuperación de la base de datos '%.*ls' (%d) se detectó una posible incoherencia de valores de identidad en la tabla con id. %d. Ejecute DBCC CHECKIDENT ("%.\*ls").|  
  
## <a name="explanation"></a>Explicación  
Durante la actualización a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], el proceso de recuperación de los valores de identidad de la base de datos detectó una incoherencia en los metadatos.  
  
## <a name="user-action"></a>Acción del usuario  
Ejecute DBCC CHECKIDENT.  
  
