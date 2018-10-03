---
title: Propiedad ConnectionPoolSize (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- ConnectionPoolSize
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- ConnectionPoolSize property
ms.assetid: b80c8e5d-b725-4fe4-aec6-02fb18ec4434
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: f4f555db5b87e2233229215da5b800c0eedea61c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48172085"
---
# <a name="connectionpoolsize-property-wmi-msreportserverconfigurationsetting"></a>Propiedad ConnectionPoolSize (WMI MSReportServer_ConfigurationSetting)
  Tamaño de grupo de conexiones utilizado por el servidor de informes para comunicarse con la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda la base de datos del servidor de informes. Solo lectura.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Dim ConnectionPoolSize As UInt32  
```  
  
```csharp  
public UInt32 ConnectionPoolSize;  
```  
  
## <a name="property-values"></a>Valores de propiedad  
 Solo lectura **entero** objeto que devuelve un valor de `768`.  
  
## <a name="example-code"></a>Código de ejemplo  
 [Clase MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
