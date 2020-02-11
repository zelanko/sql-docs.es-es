---
title: Propiedad ExitCode (clase SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- ExitCode Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- ExitCode property
ms.assetid: e6b8bff2-946f-4abe-bd50-1f7bb11fdddf
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 7a74c48cf512f33862f41484a5fb667918e81787
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63062493"
---
# <a name="exitcode-property-sqlservice-class"></a>Propiedad ExitCode (clase SqlService)
  Obtiene o establece el código de error de Win32 de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] que define los problemas encontrados al iniciar y detener el servicio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object  
.ExitCode [= value]  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 Objeto de la [clase SqlService](sqlservice-class.md) que representa el servicio.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor de `uint32` que especifica el código de salida.  
  
## <a name="remarks"></a>Observaciones  
 Esta propiedad se establece en ERROR_SERVICE_SPECIFIC_ERROR (1066) si el error es exclusivo del servicio representado por esta clase. El servicio establece este valor en NO_ERROR cuando se ejecuta y también cuando finaliza normalmente.  
  
## <a name="see-also"></a>Consulte también  
 [Iniciar y detener servicios](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
