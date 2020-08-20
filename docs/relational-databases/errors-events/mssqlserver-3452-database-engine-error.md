---
description: MSSQLSERVER_3452
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
ms.openlocfilehash: 5eaf8a280ebc3da3c1313010d336f5fa0ef67c1a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456200"
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
  
