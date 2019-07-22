---
title: MSSQLSERVER_7901 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7901 (Database Engine error)
ms.assetid: 2d0d19b9-947b-4474-9ff8-7e03019ab93d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1a10e03f2dc09bb53078faaaaea36c60e313e0eb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67951563"
---
# <a name="mssqlserver7901"></a>MSSQLSERVER_7901
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|7901|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC2_DATABASE_IN_EMERGENCY_MODE|  
|Texto del mensaje|Instrucción de reparación no procesada. No se permite este nivel de reparación cuando la base de datos está en modo de emergencia.|  
  
## <a name="explanation"></a>Explicación  
La base de datos está en modo de emergencia y se ha especificado un nivel de reparación distinto de REPAIR_ALLOW_DATA_LOSS. Las reparaciones no pueden llevarse a cabo en el modo de emergencia, a menos que se especifique REPAIR_ALLOW_DATA_LOSS.  
  
## <a name="user-action"></a>Acción del usuario  
Vuelva a ejecutar el comando y especifique la opción REPAIR_ALLOW_DATA_LOSS.  
  
