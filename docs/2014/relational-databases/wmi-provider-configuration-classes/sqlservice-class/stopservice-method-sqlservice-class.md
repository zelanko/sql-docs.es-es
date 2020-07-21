---
title: Método StopService (clase SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- StopService Method (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- StopService method
ms.assetid: ef8e1856-4930-417a-8f52-be470fd3f15c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 534db69b9c5474638ef5e893847f7d6b9bbb645d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85061320"
---
# <a name="stopservice-method-sqlservice-class"></a>Método StopService (clase SqlService)
  Intenta poner el servicio en estado de detención.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object  
.StopService()  
  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Objeto de la [clase SqlService](sqlservice-class.md) que representa el servicio.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor de `uint32` que es igual a 0 si se aceptó la solicitud de `ResumeService`, igual a 1 si no se admite dicha solicitud e igual a cualquier otro número para indicar que hubo un error.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Consulte también  
 [Iniciar y detener servicios](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
