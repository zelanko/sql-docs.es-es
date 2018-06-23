---
title: MSSQLSERVER_9692 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 9692 (Database Engine error)
ms.assetid: 02399d6e-ab5e-4f30-8a3e-2bb1e8c135b5
caps.latest.revision: 16
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 396f1ae8e711157bc8f6b911997557f68e397c47
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113592"
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
 Ejecute `netstat -aon` para determinar qué programa está usando el puerto. Deshabilite esa aplicación o especifique otro puerto para Service Broker.  
  
  