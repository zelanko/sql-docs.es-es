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
ms.openlocfilehash: ff26dbe89f4d364fcdf7fc2eca1c4d483afc68bf
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553272"
---
# <a name="mssqlserver_7915"></a>MSSQLSERVER_7915
    
## <a name="details"></a>Detalles  
  
|Atributo|Value|  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|7915|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC2_REPAIR_IAM_CHAIN_REBUILT|  
|Texto del mensaje|Reparación: la cadena de IAM para el id. de objeto O_ID, id. de índice I_ID, id. de partición PN_ID, id. de unidad de asignación A_ID (tipo TYPE), se ha truncado antes de la página P_ID y se volverá a generar.|  
  
## <a name="explanation"></a>Explicación  
 Se trata de un mensaje informativo enviado por REPAIR que indica que la cadena IAM (Mapa de asignación de índices) especificada se revisó para que pudiera volver a generarse. Esta revisión puede haber necesitado de la asignación de un nuevo encabezado de la cadena IAM o de la eliminación de las páginas erróneas de la cadena.  
  
## <a name="user-action"></a>Acción del usuario  
 None  
  
  
