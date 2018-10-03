---
title: MSSQLSERVER_617 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 617 (Database Engine error)
ms.assetid: 213545d9-08a7-4427-bfd1-8b7e16644281
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ddc9dc3cd32bae96165e29399ef99c2d428b3585
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47801911"
---
# <a name="mssqlserver617"></a>MSSQLSERVER_617
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|617|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|NODESHASH|  
|Texto del mensaje|No se encontró el descriptor del id. de objeto %ld del id. de base de datos %d en la tabla hash al intentar deshacer el hash. Falta una entrada en una tabla de trabajo. Vuelva a ejecutar la consulta. Si hay un cursor en el proceso, ciérrelo y vuelva a abrirlo.|  
  
## <a name="explanation"></a>Explicación  
SQL Server no puede encontrar la tabla de trabajo para una entrada concreta.  
  
## <a name="user-action"></a>Acción del usuario  
  
1.  Si hay un cursor en el proceso, ciérrelo y vuelve a abrirlo.  
  
2.  Ejecute de nuevo la consulta.  
  
