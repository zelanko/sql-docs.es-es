---
title: "Método SetDefaults (clase SInstance) | Documentos de Microsoft"
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
apiname: SetDefaults Method (SInstance Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: SetDefaults method
ms.assetid: dc3c6a85-0711-4688-bf4f-91168c57af28
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6311ad091e2c66bbe4d110f063c1dcd9324ef5b7
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="setdefaults-method-sinstance-class"></a>Método SetDefaults (clase SInstance)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]Establece todos los valores predeterminados para la instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con la opción para sobrescribir los datos existentes.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 Un [clase SInstance](../../../relational-databases/wmi-provider-configuration-classes/sinstance-class/sinstance-class.md) objeto que representa una instancia del servidor.  
  
#### <a name="parameters"></a>Parámetros  
  
|Parámetro|Description|  
|---------------|-----------------|  
|*OverwriteAll*|Un valor booleano que especifica si se debe sobrescribir el valor existente en la instancia de la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cliente: **true** si se sobrescriben los datos existentes o **false** si no se sobrescriben los datos existentes.|  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad/Valor devuelto  
 Valor **uint32** que es 0 si se modificó el servicio correctamente, 1 si no se admite la solicitud y cualquier otro número para indicar un error.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Configurar protocolos de red de servidor y bibliotecas de red](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
