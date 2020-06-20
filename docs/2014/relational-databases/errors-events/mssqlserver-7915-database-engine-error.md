---
title: MSSQLSERVER_7915 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 7915 (Database Engine error)
ms.assetid: 63338587-7dd3-40e6-b70e-d8ae18fff47b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e1dc7a69023e49b48a10da9f0388cbd72fbe46be
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85053721"
---
# <a name="mssqlserver_7915"></a>MSSQLSERVER_7915
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|7915|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC2_REPAIR_IAM_CHAIN_REBUILT|  
|Texto del mensaje|Reparación: la cadena de IAM para el Id. de objeto P_ID, Id. de índice I_ID, Id. de partición PN_ID, Id. de unidad de asignación ID A_ID (tipo TYPE), se ha truncado antes de la página P_ID y se volverá a generar.|  
  
## <a name="explanation"></a>Explicación  
 Se trata de un mensaje informativo enviado por REPAIR que indica que la cadena IAM (Mapa de asignación de índices) especificada se revisó para que pudiera volver a generarse. Esta revisión puede haber necesitado de la asignación de un nuevo encabezado de la cadena IAM o de la eliminación de las páginas erróneas de la cadena.  
  
## <a name="user-action"></a>Acción del usuario  
 None  
  
  
