---
title: MSSQLSERVER_8966 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8966 (Database Engine error)
ms.assetid: 6b1150fd-9dfd-4df9-8f08-8eca237667db
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d5510ea39e741e8226c976bae517e24eac99dcb7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47632343"
---
# <a name="mssqlserver8966"></a>MSSQLSERVER_8966
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
