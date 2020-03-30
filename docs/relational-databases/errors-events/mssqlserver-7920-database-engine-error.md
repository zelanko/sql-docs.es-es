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
ms.openlocfilehash: 01a6de1a94b3ea771e0d834ee815930a50b68056
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68125509"
---
# <a name="mssqlserver_7920"></a>MSSQLSERVER_7920
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|7920|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC2_SUMMARY_ENTRIES|  
|Texto del mensaje|Se han procesado ENTRY_COUNT entradas en el catálogo del sistema para el id. de base de datos D_ID.|  
  
## <a name="explanation"></a>Explicación  
Se trata de un mensaje informativo que devuelven todos los comandos DBCC CHECK excepto DBCC CHECKALLOC. El valor devuelto es el número total de conjuntos de filas comprobados.  
  
## <a name="user-action"></a>Acción del usuario  
None  
  
