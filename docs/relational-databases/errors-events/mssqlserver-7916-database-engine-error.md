---
title: MSSQLSERVER_7916 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7916 (Database Engine error)
ms.assetid: 9bac3536-de14-4e98-84c2-bde9a59ba0d1
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4ee6bae9798ab9e3c4a12f5b535c07a2a167a8ac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125515"
---
# <a name="mssqlserver7916"></a>MSSQLSERVER_7916
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|7916|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC2_REPAIR_RECORD|  
|Texto del mensaje|Reparación: se ha eliminado el registro para el id. de objeto O_ID, id. de índice I_ID, id. de partición PN_ID, id. de unidad de asignación A_ID (tipo TYPE), en la página P_ID, ranura S_ID. Se volverán a generar los índices.|  
  
## <a name="explanation"></a>Explicación  
Este es un mensaje informativo de REPAIR que indica que el registro especificado se eliminó de la página.  
  
## <a name="user-action"></a>Acción del usuario  
None  
  
