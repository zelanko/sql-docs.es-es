---
title: MSSQLSERVER_9692 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 9692 (Database Engine error)
ms.assetid: 02399d6e-ab5e-4f30-8a3e-2bb1e8c135b5
caps.latest.revision: "15"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 2c7e9da124ed3ec2fb1a0725f2f2c3050cd3484f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver9692"></a>MSSQLSERVER_9692
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|9692|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SB2_CANT_LISTEN_PORT_IN_USE|  
|Texto del mensaje|El transporte de protocolo %S_MSG no puede escuchar en el puerto %d porque lo está utilizando otro proceso.|  
  
## <a name="explanation"></a>Explicación  
Otro programa del equipo está usando el puerto TCP indicado.  
  
## <a name="user-action"></a>Acción del usuario  
Ejecute **netstat -aon** para determinar qué programa está usando el puerto. Deshabilite esa aplicación o especifique otro puerto para Service Broker.  
  
