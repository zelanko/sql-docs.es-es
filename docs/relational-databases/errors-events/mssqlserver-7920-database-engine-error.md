---
title: MSSQLSERVER_7920 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7920 (Database Engine error)
ms.assetid: d16290ea-3875-4148-8d53-057bfee00438
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 97855e4cc5b0bd9e28ef2de69622291ff175cc88
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62797128"
---
# <a name="mssqlserver7920"></a>MSSQLSERVER_7920
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|7920|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC2_SUMMARY_ENTRIES|  
|Texto del mensaje|Se han procesado ENTRY_COUNT entradas en el catálogo del sistema para el id. de base de datos D_ID.|  
  
## <a name="explanation"></a>Explicación  
Se trata de un mensaje informativo que devuelven todos los comandos DBCC CHECK excepto DBCC CHECKALLOC. El valor devuelto es el número total de conjuntos de filas comprobados.  
  
## <a name="user-action"></a>Acción del usuario  
None  
  
