---
title: Propiedad AcceptStop (clase SqlService) | Documentos de Microsoft
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
api_name:
- AcceptStop Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- AcceptStop property
ms.assetid: bf8ffe79-4f4c-4a2d-82e5-2ae8f5d466c5
caps.latest.revision: 35
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 19197db0e6d2679d0ad13bcb43472be4448fccb7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113303"
---
# <a name="acceptstop-property-sqlservice-class"></a>Propiedad AcceptStop (clase SqlService)
  Obtiene el valor de propiedad booleano que especifica si se puede detener el servicio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object  
.AcceptStop [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 A [clase SqlService](sqlservice-class.md) objeto que representa el servicio  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor booleano que especifica si se puede detener el servicio: `true` si se puede detener el servicio; en caso contrario, `false`.  
  
## <a name="remarks"></a>Notas  
  
## <a name="see-also"></a>Vea también  
 [Iniciar y detener servicios](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  