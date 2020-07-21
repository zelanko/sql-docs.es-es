---
title: Propiedad ErrorControl (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ErrorControl Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ErrorControl property
ms.assetid: cbb1e0fa-5bfc-4b1b-a6ed-f7d5cfad4d73
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 85d6031a98359cf83d0c161efd22f31a2bbe6dc7
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85880615"
---
# <a name="errorcontrol-property-sqlservice-class"></a>Propiedad ErrorControl (clase SqlService)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Obtiene o establece la gravedad del error si el servicio no se puede iniciar durante el inicio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.ErrorControl [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Objeto de la [clase SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) que representa el servicio.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor de cadena que especifica la gravedad del error notificado si se produce un error en el servicio durante el inicio. En la siguiente tabla se muestran los valores posibles.  
  
 Ignorar  
 No se notifica al usuario.  
  
 Normal  
 Se notifica al usuario.  
  
 Grave  
 El sistema se reinicia con la última configuración válida conocida.  
  
 Crítica  
 El sistema intenta reiniciarse con una configuración válida.  
  
 Desconocido  
 Se desconoce la gravedad.  
  
## <a name="remarks"></a>Comentarios  
 El valor indica la acción realizada por el programa de inicio si se produce un error. El sistema registra todos los errores.  
  
## <a name="see-also"></a>Consulte también  
 [Iniciar y detener servicios](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
