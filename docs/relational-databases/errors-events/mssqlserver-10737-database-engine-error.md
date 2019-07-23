---
title: MSSQLSERVER_10737 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10737 (Database Engine error)
ms.assetid: 208af6ed-b271-4ab8-803e-7666025385c8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 58a6ff1dda1e0694e17d891502c7dca9ebb31c8a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060581"
---
# <a name="mssqlserver10737"></a>MSSQLSERVER_10737
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
