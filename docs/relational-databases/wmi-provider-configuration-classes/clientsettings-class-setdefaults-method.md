---
title: "Método SetDefaults (clase ClientSettings) | Documentos de Microsoft"
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
apiname: SetDefaults Method (ClientSettings Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: SetDefaults method
ms.assetid: 056508f3-a5c8-467c-a196-dc1ef1f5178f
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b86a8301664f483c339f020cf0a8de5c2803749b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="clientsettings-class---setdefaults-method"></a>Clase ClientSettings - SetDefaults, método
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]Establece todos los valores predeterminados para la instancia de la [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cliente con la opción para sobrescribir los datos existentes.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 A **ClientSettings** objeto que representa un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia del cliente.  
  
#### <a name="parameters"></a>Parámetros  
  
|Parámetro|Description|  
|---------------|-----------------|  
|*OverwriteAll*|Valor booleano que especifica si se van a sobrescribir los valores existentes en la instancia del cliente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. **true** si se van a sobrescribir los datos existentes; **false** si no se van a sobrescribir.|  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad/Valor devuelto  
 Valor **uint32** que es 0 si se modificó el servicio correctamente, 1 si no se admite la solicitud y cualquier otro número para indicar un error.  
  
## <a name="remarks"></a>Comentarios  
  
