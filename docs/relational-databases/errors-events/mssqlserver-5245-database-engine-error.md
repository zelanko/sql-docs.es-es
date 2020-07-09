---
title: MSSQLSERVER_5245 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5245 (Database Engine error)
ms.assetid: 6005c9ec-ccdd-4def-9eb4-37cdb599ddb3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a2981d59b8bcc21d9a21fe0fd707cfcb9278cc57
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717002"
---
# <a name="mssqlserver_5245"></a>MSSQLSERVER_5245
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
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
  
