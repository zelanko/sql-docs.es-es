---
title: LOCALDB_ERROR_INSUFFICIENT_BUFFER | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: ff67bda8-7e5c-4b06-8d7b-9985b6059a98
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 48ea53756395c717ec716e35787371ada260d894
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105856"
---
# <a name="localdberrorinsufficientbuffer"></a>LOCALDB_ERROR_INSUFFICIENT_BUFFER
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|276|  
|Origen del evento|SQL Server Local Database Runtime 12.0|  
|Componente|API de Local Database Runtime|  
|Texto del mensaje|El búfer pasado el método de API de la instancia de Local Database no tiene un tamaño suficiente.|  
  
## <a name="explanation"></a>Explicación  
 El búfer de entrada es demasiado corto y no se ha solicitado truncamiento.  
  
## <a name="user-action"></a>Acción del usuario  
 Proporcione un búfer del tamaño especificado.  
  
  