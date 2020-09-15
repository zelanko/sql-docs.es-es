---
description: Propiedad SecureConnectionLevel (WMI MSReportServer_ConfigurationSetting)
title: Propiedad SecureConnectionLevel (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- SecureConnectionLevel
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SecureConnectionLevel property
ms.assetid: fd5549e7-b874-41e2-866e-2f58caf6f733
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: dcf7fdc038f5284d78835e64e568bb348756a3d7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88373161"
---
# <a name="configurationsetting-property---secureconnectionlevel"></a>Propiedad de ConfigurationSetting: SecureConnectionLevel
  Devuelve el nivel de conexión segura especificado en el archivo RSReportServer.config. Solo lectura.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Dim SecureConnectionLevel As Integer  
```  
  
```csharp  
public Integer SecureConnectionLevel;  
```  
  
## <a name="property-values"></a>Valores de propiedad  
 Un valor **Integer** que representa el nivel de conexión segura. Los valores devueltos indican si TLS está configurado o no. Un valor mayor o igual que 1 indica que TLS está activado. Un valor 0 indica que TLS está desactivado.  
  
## <a name="example-code"></a>Código de ejemplo  
 [Clase MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>Observaciones

En SQL Server 2008 R2, SecureConnectionLevel actúa como un conmutador de activación o desactivación. Para obtener más información, consulte [Método ConfigurationSetting - SetSecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setsecureconnectionlevel.md).

## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
