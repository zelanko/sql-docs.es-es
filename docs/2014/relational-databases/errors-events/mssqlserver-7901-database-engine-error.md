---
title: MSSQLSERVER_7901 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 7901 (Database Engine error)
ms.assetid: 2d0d19b9-947b-4474-9ff8-7e03019ab93d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6dd4d2721967049295f3fcf5fc8b38807268879a
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551062"
---
# <a name="mssqlserver_7901"></a>MSSQLSERVER_7901
    
## <a name="details"></a>Detalles  
  
|Atributo|Value|  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|7901|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC2_DATABASE_IN_EMERGENCY_MODE|  
|Texto del mensaje|Instrucción de reparación no procesada. No se permite este nivel de reparación cuando la base de datos está en modo de emergencia.|  
  
## <a name="explanation"></a>Explicación  
 La base de datos está en modo de emergencia y se ha especificado un nivel de reparación distinto de REPAIR_ALLOW_DATA_LOSS. Las reparaciones no pueden llevarse a cabo en el modo de emergencia, a menos que se especifique REPAIR_ALLOW_DATA_LOSS.  
  
## <a name="user-action"></a>Acción del usuario  
 Vuelva a ejecutar el comando y especifique la opción REPAIR_ALLOW_DATA_LOSS.  
  
  
