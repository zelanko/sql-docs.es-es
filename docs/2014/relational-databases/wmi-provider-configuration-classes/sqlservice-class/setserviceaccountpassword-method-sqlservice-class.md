---
title: Método SetServiceAccountPassword (clase SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetServiceAccountPassword Method (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetServiceAccountPassword method
ms.assetid: e577a1ac-985c-4799-bb38-9393efc3def2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 41823ebcbad3f545a8b516b3fad457230d3fdf8e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85067877"
---
# <a name="setserviceaccountpassword-method-sqlservice-class"></a>Método SetServiceAccountPassword (clase SqlService)
  Modifica la contraseña de la cuenta en la que se ejecuta el servicio al que se hace referencia.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object  
.SetServiceAccountPassword(  
AccountOldPassword , ServiceStartPassword  
)  
  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Objeto de la [clase SqlService](sqlservice-class.md) que representa el servicio.  
  
#### <a name="parameters"></a>Parámetros  
 *AccountOldPassword*  
 Valor de cadena que especifica la contraseña existente para la cuenta.  
  
 *ServiceStartPassword*  
 Valor de cadena que especifica la nueva contraseña para la cuenta.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor `uint32` que es 0 si se modificó el servicio correctamente, 1 si no se admite la solicitud y cualquier otro número para indicar un error.  
  
## <a name="remarks"></a>Comentarios  
  
