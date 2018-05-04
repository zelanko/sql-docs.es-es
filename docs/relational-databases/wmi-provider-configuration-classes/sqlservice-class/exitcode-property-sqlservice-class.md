---
title: Propiedad ExitCode (clase SqlService) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ExitCode Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ExitCode property
ms.assetid: e6b8bff2-946f-4abe-bd50-1f7bb11fdddf
caps.latest.revision: 34
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 07aaad1e95d5c02bbb6f82f3dfa2d26e079372f7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="exitcode-property-sqlservice-class"></a>Propiedad ExitCode (clase SqlService)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Obtiene o establece el código de error de Win32 de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] que define los problemas encontrados al iniciar y detener el servicio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.ExitCode [= value]  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 Objeto de la [clase SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) que representa el servicio.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor de **uint32** que especifica el código de salida.  
  
## <a name="remarks"></a>Comentarios  
 Esta propiedad se establece en ERROR_SERVICE_SPECIFIC_ERROR (1066) si el error es exclusivo del servicio representado por esta clase. El servicio establece este valor en NO_ERROR cuando se ejecuta y también cuando finaliza normalmente.  
  
## <a name="see-also"></a>Vea también  
 [Iniciar y detener servicios](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
