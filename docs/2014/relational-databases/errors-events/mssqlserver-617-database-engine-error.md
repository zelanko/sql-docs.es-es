---
title: MSSQLSERVER_617 | Microsoft Docs
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
- 617 (Database Engine error)
ms.assetid: 213545d9-08a7-4427-bfd1-8b7e16644281
caps.latest.revision: 14
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: a6721f3d1ab1608e3231a58535f9e59e51f5b844
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113601"
---
# <a name="mssqlserver617"></a>MSSQLSERVER_617
    
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
  
  