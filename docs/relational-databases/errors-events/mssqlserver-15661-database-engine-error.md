---
title: MSSQLSERVER_15661 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 15661 (Database Engine error)
ms.assetid: 88b01bfb-74ce-4aa0-aec0-7885261c7ef3
caps.latest.revision: 11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 513193a762e5e0deb6aa3d8fd7a02ff9f088e37a
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver15661"></a>MSSQLSERVER_15661
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|15661|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQLErrorNum15661|  
|Texto del mensaje|El procedimiento almacenado sp_estimate_data_compression_savings no se puede utilizar para las tablas temporales.|  
  
## <a name="explanation"></a>Explicación  
Se utilizó una tabla temporal como argumento para el procedimiento almacenado sp_estimate_data_compression_savings. Aunque se admite la compresión de tablas temporales, no se puede utilizar sp_estimate_data_compression_savings para estimar los ahorros obtenidos con la compresión.  
  
## <a name="user-action"></a>Acción del usuario  
Quite la tabla temporal como argumento para sp_estimate_data_compression_savings.  
  
