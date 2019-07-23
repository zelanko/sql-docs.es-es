---
title: MSSQLSERVER_11409 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 11409 (Database Engine error)
ms.assetid: 99b71a1c-a72d-4ca9-9d00-4230c9042ba5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7f4bc66c40cb6940694c1a25c4430ba3cc83e7c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68116208"
---
# <a name="mssqlserver11409"></a>MSSQLSERVER_11409
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|11409|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|ALTERCOL_COLSET_DROP|  
|Texto del mensaje|No se puede quitar el conjunto de columnas '%.*ls' de la tabla '%.\*ls' porque la tabla contiene más de 1025 columnas.|  
  
## <a name="explanation"></a>Explicación  
Las tablas pueden contener 1024 columnas, como máximo, que no estén designadas como dispersas o calculadas. Cuando las columnas dispersas hacen que la tabla supere el número de 1024 columnas, se debe definir un conjunto de columnas para la tabla. La tabla a la que se hace referencia tiene más de 1024 columnas y se ha intentado quitar el conjunto de columnas.  
  
## <a name="user-action"></a>Acción del usuario  
Con las columnas actuales en la tabla, debe conservar el conjunto de columnas.  
  
Para quitar el conjunto de columnas, primero debe quitar columnas de la tabla, hasta que haya menos de 1024. A continuación, puede quitar el conjunto de columnas.  
  
