---
title: MSSQLSERVER_17204 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 17204 (Database Engine error)
ms.assetid: 40db66f9-dd5e-478c-891e-a06d363a2552
caps.latest.revision: 14
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: e3326f262e63c658589032688c82827e86d93a9b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202717"
---
# <a name="mssqlserver17204"></a>MSSQLSERVER_17204
    
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
  
  