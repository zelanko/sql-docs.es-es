---
title: MSSQLSERVER_8966 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8966 (Database Engine error)
ms.assetid: 6b1150fd-9dfd-4df9-8f08-8eca237667db
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dee5b45aac6518517434595b0f26ce18d219866b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62913167"
---
# <a name="mssqlserver8966"></a>MSSQLSERVER_8966
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|8966|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC3_FAILED_TO_READ_AND_LATCH_PAGE|  
|Texto del mensaje|No se puede leer la página de bloqueo temporal P_ID con el tipo de bloqueo temporal TYPE. Error de OPERATION.|  
  
## <a name="explanation"></a>Explicación  
 Se produjo un error en la lectura de página o en un bloqueo temporal en una página PFS o GAM. Es posible que se haya agotado el tiempo de espera para el bloqueo temporal o existan otros mensajes asociados en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="user-action"></a>Acción del usuario  
 Revise en el registro de errores de SQL los mensajes asociados y resuelva estos errores.  
  
  
