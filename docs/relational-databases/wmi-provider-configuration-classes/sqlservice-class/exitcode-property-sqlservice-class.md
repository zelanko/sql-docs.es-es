---
title: Propiedad ExitCode (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ExitCode Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ExitCode property
ms.assetid: e6b8bff2-946f-4abe-bd50-1f7bb11fdddf
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0183882ae3544ffe23b14a848067465924748ca3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85662267"
---
# <a name="exitcode-property-sqlservice-class"></a>Propiedad ExitCode (clase SqlService)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  Obtiene o establece el código de error de Win32 de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] que define los problemas encontrados al iniciar y detener el servicio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.ExitCode [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Objeto de la [clase SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) que representa el servicio.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor de **uint32** que especifica el código de salida.  
  
## <a name="remarks"></a>Comentarios  
 Esta propiedad se establece en ERROR_SERVICE_SPECIFIC_ERROR (1066) si el error es exclusivo del servicio representado por esta clase. El servicio establece este valor en NO_ERROR cuando se ejecuta y también cuando finaliza normalmente.  
  
## <a name="see-also"></a>Consulte también  
 [Iniciar y detener servicios](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
