---
title: Propiedad DatabaseLogonTimeout (WMI MSReportServer_ConfigurationSetting) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- DatabaseLogonTimeout Property
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- DatabaseLogonTimeout property
ms.assetid: 4a65162c-33de-485e-8fd3-2bd6bff8bf8d
caps.latest.revision: 38
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: a8c1747fa53376dbe088f358cc47a13664d90bff
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="configurationsetting-property---databaselogontimeout"></a>Propiedad ConfigurationSetting - DatabaseLogonTimeout
  Especifica el número de segundos de espera antes de que se produzca un error al intentar iniciar sesión en la base de datos del servidor de informes. Si el valor es **0** , indica un período de tiempo de espera infinito. Solo lectura.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Dim DatabaseLogonTimeout As Int32  
```  
  
```csharp  
public Int32 DatabaseLogonTimeout;  
```  
  
## <a name="property-values"></a>Valores de propiedad  
 Un objeto entero de 32 bits con signo que representa el número de segundos.  
  
## <a name="example-code"></a>Código de ejemplo  
 [Clase MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
