---
title: MSSQLSERVER_10737 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10737 (Database Engine error)
ms.assetid: 208af6ed-b271-4ab8-803e-7666025385c8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: df8a4de014552d3aca00b3eb244f7ff8df56756b
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969755"
---
# <a name="mssqlserver_10737"></a>MSSQLSERVER_10737
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|MSSQLSERVER|  
|Id. de evento|10737|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|REBUILD_PARTITION_ALL_NOT_SPECIFIED|  
|Texto del mensaje|En una instrucción ALTER TABLE REBUILD o ALTER INDEX REBUILD, cuando se especifica una partición en una cláusula DATA_COMPRESSION, se debe especificar PARTITION=ALL. La cláusula PARTITION=ALL se utiliza para reforzar que se volverán a generar todas las particiones de la tabla o índice, aunque solo se especifique un subconjunto en la cláusula DATA_COMPRESSION.|  
  
## <a name="user-action"></a>Acción del usuario  
 Agregue la cláusula PARTITION=ALL a la instrucción ALTER TABLE o ALTER INDEX. O bien, para volver a generar una partición concreta, use Rebuild PARTITION = \<partition-number-expr> with (DATA_COMPRESSION = {on | OFF}).  
  
  
