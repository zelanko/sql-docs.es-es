---
description: 'Clase CInstance: método SetDefaults'
title: Método SetDefaults (CInstance)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetDefaults Method (CInstance Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetDefaults method
ms.assetid: ed9e99c2-3e28-4ee8-bc20-61ca05984973
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2a99b8bbc94bf8e62cd8125e01327a4691a296cb
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545327"
---
# <a name="cinstance-class---setdefaults-method"></a>Clase CInstance: método SetDefaults
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Establece todos los valores predeterminados para la instancia del [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cliente con la opción de sobrescribir los datos existentes.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Objeto de la [clase CInstance](../../relational-databases/wmi-provider-configuration-classes/cinstance-class.md) que representa una instancia del cliente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
#### <a name="parameters"></a>Parámetros  
  
|Parámetro|Descripción|  
|---------------|-----------------|  
|*OverwriteAll*|Valor booleano que especifica si se van a sobrescribir los valores existentes en la instancia del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cliente: **true** para sobrescribir los datos existentes o **false** si no se van a sobrescribir los datos existentes.|  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor **uint32** que es 0 si se modificó el servicio correctamente, 1 si no se admite la solicitud y cualquier otro número para indicar un error.  
  
## <a name="remarks"></a>Observaciones  
  
## <a name="see-also"></a>Consulte también  
 [Configurar protocolos de cliente](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
