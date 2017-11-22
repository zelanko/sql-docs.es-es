---
title: Propiedad ExitCode (clase SqlService) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ExitCode Property (SqlService Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: ExitCode property
ms.assetid: e6b8bff2-946f-4abe-bd50-1f7bb11fdddf
caps.latest.revision: "34"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f464d5134d0424b23086170e88054878543ff121
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="exitcode-property-sqlservice-class"></a>Propiedad ExitCode (clase SqlService)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]Obtiene o establece la [!INCLUDE[msCoName](../../../includes/msconame-md.md)] código de error de Win32 que define los problemas encontrados al iniciar y detener el servicio.  
  
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
  
  
