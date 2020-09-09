---
description: Propiedad SqlServiceType (clase SqlService)
title: Propiedad SqlServiceType (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SqlServiceType Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SqlServiceType property
ms.assetid: dbff2968-3011-41d6-a141-52d814af0213
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 685fb402647c7a757f7a894705cf7754d696b24d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542821"
---
# <a name="sqlservicetype-property-sqlservice-class"></a>Propiedad SqlServiceType (clase SqlService)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Obtiene el tipo del servicio administrado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.SqlServiceType [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Objeto de la [clase SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) que representa el servicio.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor de uint32 que especifica el tipo de servicio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
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
|*8*|NsService es el [!INCLUDE[ssNoVersion](../../../includes/ssns-md.md)] servicio de notificación.|  
|*9*|MSSQLFDLauncher es el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] servicio selector del demonio de filtro de texto completo.|  
|*10*|SQLPBENGINE es el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] servicio del motor de polybase.|  
|*11*|SQLPBDMS es el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] servicio de movimiento de datos de polybase.|  
|*12*|MSSQLLaunchpad es el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] servicio Launchpad.|  
  
## <a name="see-also"></a>Consulte también  
 [Iniciar y detener servicios](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
