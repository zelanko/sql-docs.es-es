---
title: Método ResumeService (clase SqlService) | Microsoft Docs
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
- ResumeService Method (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- ResumeService method
ms.assetid: 0b0a5f08-b95e-4626-bf81-309da7a0aacd
caps.latest.revision: 34
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 0cf92d7c4342cba1dd601e5e927c93e78aae6784
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37319757"
---
# <a name="resumeservice-method-sqlservice-class"></a>Método ResumeService (clase SqlService)
  Intenta poner el servicio en estado reanudado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object  
.ResumeService()  
  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Objeto de la [clase SqlService](sqlservice-class.md) que representa el servicio.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor unit 32 que es igual a 0 si se aceptó la solicitud de `ResumeService`, igual a 1 si no se admite dicha solicitud e igual a cualquier otro número para indicar que hubo un error.  
  
## <a name="remarks"></a>Notas  
  
## <a name="see-also"></a>Vea también  
 [Iniciar y detener servicios](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
