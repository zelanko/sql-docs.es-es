---
description: Propiedad ExitCode (clase SqlService)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 71e5fbe4180c67560709f004ba099bb90ca83b02
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542860"
---
# <a name="exitcode-property-sqlservice-class"></a>Propiedad ExitCode (clase SqlService)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
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
  
## <a name="remarks"></a>Observaciones  
 Esta propiedad se establece en ERROR_SERVICE_SPECIFIC_ERROR (1066) si el error es exclusivo del servicio representado por esta clase. El servicio establece este valor en NO_ERROR cuando se ejecuta y también cuando finaliza normalmente.  
  
## <a name="see-also"></a>Consulte también  
 [Iniciar y detener servicios](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
