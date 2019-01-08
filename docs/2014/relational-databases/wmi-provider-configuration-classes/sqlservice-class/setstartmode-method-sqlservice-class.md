---
title: Método SetStartMode (clase SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetStartMode Method (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetStartMode method
ms.assetid: f6f198b4-f9a4-468c-8977-76462ef06e61
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 0b3689c843fbbe7ad845a45aca6bb962f8f0c75e
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53371677"
---
# <a name="setstartmode-method-sqlservice-class"></a>Método SetStartMode (clase SqlService)
  Modifica el modo de inicio de la instancia del servicio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object  
.SetStartMode(  
StartMode  
)  
  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Objeto de la [clase SqlService](sqlservice-class.md) que representa el servicio.  
  
#### <a name="parameters"></a>Parámetros  
 *StartMode*  
 Valor de `uint32` que especifica el modo de inicio de la instancia del servicio.  
  
 Los valores válidos son los siguientes:  
  
 Valor = 0. Boot: controlador de dispositivo iniciado por el cargador del sistema operativo. Este valor solamente es válido para servicios de controladores.  
  
 Valor = 1. System: controlador de dispositivo iniciado por el método `IoInitSystem`. Este valor solamente es válido para servicios de controladores.  
  
 Valor = 2. Automatic: servicio que el administrador de control de servicios iniciará automáticamente durante el inicio del sistema.  
  
 Valor = 3. Manual: servicio que el administrador de equipo iniciará cuando un proceso llame al método `StartService`.  
  
 Valor = 4. Disabled: el servicio ya no se puede iniciar.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor de `uint32` que es igual a 0 si se modificó el servicio correctamente o igual a 1 si no se admite la solicitud. Cualquier otro número indica que hubo un error.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Iniciar y detener servicios](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
