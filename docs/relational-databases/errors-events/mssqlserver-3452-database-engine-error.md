---
title: MSSQLSERVER_3452 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3452 (Database Engine error)
ms.assetid: bf838f02-7186-4b33-b01e-361b0c02de1f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 775a141774bf8974aa874f7879ce3b65694cf17d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723494"
---
# <a name="mssqlserver_3452"></a>MSSQLSERVER_3452
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|3452|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|REC_CHECKIDENTITY|  
|Texto del mensaje|En la recuperación de la base de datos '%.*ls' (%d) se detectó una posible incoherencia de valores de identidad en la tabla con id. %d. Ejecute DBCC CHECKIDENT ("%.\*ls").|  
  
## <a name="explanation"></a>Explicación  
Durante la actualización a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], el proceso de recuperación de los valores de identidad de la base de datos detectó una incoherencia en los metadatos.  
  
## <a name="user-action"></a>Acción del usuario  
Ejecute DBCC CHECKIDENT.  
  
