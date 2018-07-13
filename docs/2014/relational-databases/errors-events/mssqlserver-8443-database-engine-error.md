---
title: MSSQLSERVER_8443 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 8443 (Database Engine error)
ms.assetid: a3541b9c-b1a8-4280-add1-275f08696b62
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2e2f275c073750ba3998299c41375d8ecc5eb6ea
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37414364"
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
  
  
