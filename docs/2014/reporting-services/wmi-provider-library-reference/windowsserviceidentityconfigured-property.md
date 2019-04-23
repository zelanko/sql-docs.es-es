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
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3e457229b44a2d3176fe6c36d825f86dd917c47b
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59943573"
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
  
  
