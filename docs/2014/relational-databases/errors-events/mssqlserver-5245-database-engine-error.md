---
title: MSSQLSERVER_5245 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 5245 (Database Engine error)
ms.assetid: 6005c9ec-ccdd-4def-9eb4-37cdb599ddb3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2cea5c900150a26ecde783e50b953cc4a035a8ff
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551222"
---
# <a name="mssqlserver_5245"></a>MSSQLSERVER_5245
    
## <a name="details"></a>Detalles  
  
|Atributo|Value|  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|5245|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC4_TABLE_LOCK_TIMEOUT_EXCEEDED|  
|Texto del mensaje|Id. de objeto O_ID (objeto "NAME"): DBCC no pudo obtener un bloqueo en este objeto porque se superó el tiempo de espera de la solicitud de bloqueo. Este objeto ha sido omitido y no se va a procesar.|  
  
## <a name="explanation"></a>Explicación  
 Se produjo un tiempo de espera de bloqueo mientras DBCC estaba esperando un bloqueo de tabla para el objeto especificado.  
  
## <a name="user-action"></a>Acción del usuario  
 Vuelva a ejecutar el comando DBCC.  
  
  
