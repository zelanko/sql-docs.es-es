---
title: MSSQLSERVER_7915 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7915 (Database Engine error)
ms.assetid: 63338587-7dd3-40e6-b70e-d8ae18fff47b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 653deb1710937d37a11688d41eb378c0650e0a20
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47803483"
---
# <a name="mssqlserver7915"></a>MSSQLSERVER_7915
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|7915|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC2_REPAIR_IAM_CHAIN_REBUILT|  
|Texto del mensaje|Reparación: la cadena de IAM para el Id. de objeto P_ID, Id. de índice I_ID, Id. de partición PN_ID, Id. de unidad de asignación ID A_ID (tipo TYPE), se ha truncado antes de la página P_ID y se volverá a generar.|  
  
## <a name="explanation"></a>Explicación  
Se trata de un mensaje informativo enviado por REPAIR que indica que la cadena IAM (Mapa de asignación de índices) especificada se revisó para que pudiera volver a generarse. Esta revisión puede haber necesitado de la asignación de un nuevo encabezado de la cadena IAM o de la eliminación de las páginas erróneas de la cadena.  
  
## <a name="user-action"></a>Acción del usuario  
None  
  
