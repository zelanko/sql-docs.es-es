---
title: MSSQLSERVER_12329 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 12329 (Database Engine error)
ms.assetid: 43f90287-36d5-46c2-ac91-a37202dcf6d3
caps.latest.revision: 4
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a2564cec904ae7e587bd91bc69e51c3c8b09e1c5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver12329"></a>MSSQLSERVER_12329
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|12329|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|HK_UNSUPPORTED_NON_LATIN_CODEPAGE|  
|Texto del mensaje|Los tipos de datos char(n) y varchar(n) que usan una intercalación con una página de códigos distinta de 1252 no se admiten con *construct*.|  
  
## <a name="explanation"></a>Explicación  
No use los tipos de datos char(n) y varchar(n) que usan una intercalación con una página de códigos distinta de 1252.  
  
## <a name="user-action"></a>Acción del usuario  
Una situación inesperada que puede producir este error es:  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = 'us_english')  
```  
  
Use esto en su lugar:  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
```  
  
