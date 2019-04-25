---
title: MSSQLSERVER_7911 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7911 (Database Engine error)
ms.assetid: dd8390f3-0f77-4fb2-ba94-631a56e42bc6
author: MashaMSFT
ms.author: mathoma
manager: craigg
robots: noindex,nofollow
ms.openlocfilehash: dbb5a12fdcb3c326957d719882feec4fe948190c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62761845"
---
# <a name="mssqlserver7911"></a>MSSQLSERVER_7911
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|7911|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC2_REPAIR_PAGE_DEALLOCATED|  
|Texto del mensaje|Reparación: La página P_ID se ha desasignado de objeto ID O_ID, index ID. de partición PN_ID, unidad de asignación A_ID (tipo TYPE).|  
  
## <a name="explanation"></a>Explicación  
Se trata de un mensaje informativo de REPAIR en el que se indica que se ha cancelado la asignación de una página de la matriz de espacios asignados en una página IAM (Mapa de asignación de índices).  
  
## <a name="user-action"></a>Acción del usuario  
None  
  
