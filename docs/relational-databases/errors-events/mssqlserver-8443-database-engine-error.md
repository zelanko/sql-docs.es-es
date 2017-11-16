---
title: MSSQLSERVER_8443 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 8443 (Database Engine error)
ms.assetid: a3541b9c-b1a8-4280-add1-275f08696b62
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: add01087d5bd0e5b2daecb2eeab2981873f8748b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver8443"></a>MSSQLSERVER_8443
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|8443|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SB_DIALOG_WO_CONV_GROUP|  
|Texto del mensaje|La conversación con id. '%.*ls' y el iniciador %d hace referencia a un grupo de conversaciones que falta ('%.\*ls'). Ejecute DBCC CHECKDB para analizar y reparar la base de datos.|  
  
## <a name="explanation"></a>Explicación  
La capa de metadatos devolvió NULL para el grupo de conversaciones. La base de datos ha resultado dañada de alguna manera. Un posible origen de los daños es un error de disco.  
  
## <a name="user-action"></a>Acción del usuario  
Ejecute DBCC CHECKDB en el modo de reparación para restaurar la base de datos a un estado coherente. Puede que se eliminen mensajes si es necesario para restablecer la coherencia. Investigue en los registros de errores del sistema para ver si la causa de este error es otro error del sistema.  
  
