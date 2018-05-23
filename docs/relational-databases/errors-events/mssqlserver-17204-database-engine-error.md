---
title: MSSQLSERVER_17204 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 17204 (Database Engine error)
ms.assetid: 40db66f9-dd5e-478c-891e-a06d363a2552
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c71de5b96a2b849e17c919980b096678bd772b7e
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver17204"></a>MSSQLSERVER_17204
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|17204|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBLKIO_DEVOPENFAILED|  
|Texto del mensaje|%ls: no se pudo abrir el archivo %ls para el número de archivo %d.  Error del sistema operativo: %ls.|  
  
## <a name="explanation"></a>Explicación  
SQL Server no pudo abrir el archivo especificado debido al error indicado.  
  
## <a name="user-action"></a>Acción del usuario  
Diagnostique y corrija el problema del sistema operativo y, a continuación, vuelva a intentar la operación.  
  
