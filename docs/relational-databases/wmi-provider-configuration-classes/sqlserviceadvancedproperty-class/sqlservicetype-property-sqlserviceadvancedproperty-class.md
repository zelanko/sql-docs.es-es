---
title: Propiedad SqlServiceType (SqlServiceAdvancedProperty)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SqlServiceType Property (SqlServiceAdvancedProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SqlServiceType property
ms.assetid: 20f1663a-9a14-4f14-8c1b-8aa133e272c3
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 59c42bdb98d5ed19ea2d415a85e9d2ccb4aeb8b2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "73658965"
---
# <a name="sqlservicetype-property-sqlserviceadvancedproperty-class"></a>Propiedad SqlServiceType (clase SqlServiceAdvancedProperty)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Obtiene el tipo del servicio administrado que está asociado a la propiedad avanzada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.SetBoolValue(NumValue)  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 Objeto de la [clase SqlServiceAdvancedProperty](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) que representa una propiedad avanzada.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor uint32 que especifica el tipo de servicio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="remarks"></a>Observaciones  
 Los valores devueltos pueden ser uno de los siguientes:  
  
|Tipo|Definición|  
|----------|----------------|  
|*1*|MSSQLSERVER es el servicio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|*2*|SQLSERVERAGENT es el servicio Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|*3*|MSFTESQL es el servicio de motor de búsqueda de texto completo de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|*4*|MsDtsServer es el servicio [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] .|  
|*5*|MSSQLServerOLAPService es el servicio [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .|  
|*6*|ReportServer es el servicio [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] .|  
|*7*|SQLBrowser es el servicio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Browser.|  
|*203*|NsService es el [!INCLUDE[ssNoVersion](../../../includes/ssns-md.md)] servicio de notificación.|  
|*9*|MSSQLFDLauncher es el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] servicio selector del demonio de filtro de texto completo.|  
|*7*|SQLPBENGINE es el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] servicio del motor de polybase.|  
|*11*|SQLPBDMS es el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] servicio de movimiento de datos de polybase.|  
|*12*|MSSQLLaunchpad es el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] servicio Launchpad.|  
  
## <a name="see-also"></a>Consulte también  
 [Iniciar y detener servicios](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
