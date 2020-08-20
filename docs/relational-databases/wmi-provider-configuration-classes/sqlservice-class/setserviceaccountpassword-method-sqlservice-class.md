---
description: Método SetServiceAccountPassword (clase SqlService)
title: Método SetServiceAccountPassword (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetServiceAccountPassword Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetServiceAccountPassword method
ms.assetid: e577a1ac-985c-4799-bb38-9393efc3def2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 18f83f130abc935bdfcff62d2f3b46087ee83a48
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488403"
---
# <a name="setserviceaccountpassword-method-sqlservice-class"></a>Método SetServiceAccountPassword (clase SqlService)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Modifica la contraseña de la cuenta en la que se ejecuta el servicio al que se hace referencia.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.SetServiceAccountPassword(AccountOldPassword , ServiceStartPassword)  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Objeto de la [clase SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) que representa el servicio.  
  
#### <a name="parameters"></a>Parámetros  
 *AccountOldPassword*  
 Valor de cadena que especifica la contraseña existente para la cuenta.  
  
 *ServiceStartPassword*  
 Valor de cadena que especifica la nueva contraseña para la cuenta.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor **uint32** que es 0 si se modificó el servicio correctamente, 1 si no se admite la solicitud y cualquier otro número para indicar un error.  
  
## <a name="remarks"></a>Observaciones  
  
