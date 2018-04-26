---
title: MSSQLSERVER_17053 | Microsoft Docs
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
- 17053 (Database Engine error)
ms.assetid: e0a01f3d-d0aa-4c38-8bcc-82e59de50512
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8fa2aabfa00f75a7abb4407dcb88cb2b75f41d69
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver17053"></a>MSSQLSERVER_17053
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|17053|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|OS_ERROR|  
|Texto del mensaje|% ls: error %ls del sistema operativo.|  
  
## <a name="explanation"></a>Explicación  
Se produjo un error genérico del sistema operativo.  No está claro cuál es el estado resultante.  
  
## <a name="user-action"></a>Acción del usuario  
Normalmente este error se produce junto con algún otro y se debería usar como ayuda para diagnosticar dicho error. Algunos ejemplos incluirían las lecturas o escrituras de datos o archivos de registro en los que se producen errores, operaciones de lectura y escritura en el Registro u otros errores inesperados de Win32API.  
  
