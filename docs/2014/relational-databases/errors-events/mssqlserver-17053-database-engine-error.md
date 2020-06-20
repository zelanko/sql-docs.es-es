---
title: MSSQLSERVER_17053 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17053 (Database Engine error)
ms.assetid: e0a01f3d-d0aa-4c38-8bcc-82e59de50512
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 11137ba334b66f20c7d9a6caaaf7d1ef42c15dec
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969485"
---
# <a name="mssqlserver_17053"></a>MSSQLSERVER_17053
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|17053|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|OS_ERROR|  
|Texto del mensaje|% ls: error %ls del sistema operativo.|  
  
## <a name="explanation"></a>Explicación  
 Se produjo un error genérico del sistema operativo.  No está claro cuál es el estado resultante.  
  
## <a name="user-action"></a>Acción del usuario  
 Normalmente este error se produce junto con algún otro y se debería usar como ayuda para diagnosticar dicho error. Algunos ejemplos incluirían las lecturas o escrituras de datos o archivos de registro en los que se producen errores, operaciones de lectura y escritura en el Registro u otros errores inesperados de Win32API.  
  
  
