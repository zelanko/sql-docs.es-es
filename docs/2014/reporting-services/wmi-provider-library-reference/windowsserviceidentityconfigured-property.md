---
title: Propiedad WindowsServiceIdentityConfigured (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- WindowsServiceIdentityConfigured
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WindowsServiceIdentityConfigured property
ms.assetid: ebf8e559-7fe4-4a01-9810-85f18fc04596
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: dc50326b1ac8788344c6d8fa00b8d7187d17ca11
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48189835"
---
# <a name="windowsserviceidentityconfigured-property-wmi-msreportserverconfigurationsetting"></a>Propiedad WindowsServiceIdentityConfigured (MSReportServer_ConfigurationSetting de WMI)
  Devuelve la última identidad en la que se configuró el servicio Servidor de informes de Windows para ejecutarse. Solo lectura.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Dim WindowsServiceIdentityConfigured As String  
```  
  
```csharp  
public string WindowsServiceIdentityConfigured;  
```  
  
## <a name="property-values"></a>Valores de propiedad  
 Un valor `String` que contiene la identidad en que el servicio Windows del servidor de informes fue configurado por última vez para ejecutarse.  
  
## <a name="example-code"></a>Código de ejemplo  
 [Clase MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
