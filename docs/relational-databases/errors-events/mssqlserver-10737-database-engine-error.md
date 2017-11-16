---
title: MSSQLSERVER_10737 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 10737 (Database Engine error)
ms.assetid: 208af6ed-b271-4ab8-803e-7666025385c8
caps.latest.revision: "10"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: a5fef9ff1b72130ae5cb935a27e5ad82fc616d66
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver10737"></a>MSSQLSERVER_10737
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|MSSQLSERVER|  
|Identificador del evento|10737|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|REBUILD_PARTITION_ALL_NOT_SPECIFIED|  
|Texto del mensaje|En una instrucción ALTER TABLE REBUILD o ALTER INDEX REBUILD, cuando se especifica una partición en una cláusula DATA_COMPRESSION, se debe especificar PARTITION=ALL. La cláusula PARTITION=ALL se utiliza para reforzar que se volverán a generar todas las particiones de la tabla o índice, aunque solo se especifique un subconjunto en la cláusula DATA_COMPRESSION.|  
  
## <a name="user-action"></a>Acción del usuario  
Agregue la cláusula PARTITION=ALL a la instrucción ALTER TABLE o ALTER INDEX. O bien, para volver a generar una partición concreta, use REBUILD PARTITION = \<expresiónDeNúmeroDePartición> WITH (DATA_COMPRESSION={ON | OFF}).  
  
