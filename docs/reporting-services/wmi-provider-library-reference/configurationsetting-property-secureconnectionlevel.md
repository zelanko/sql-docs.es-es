---
title: Propiedad SecureConnectionLevel (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: wmi-provider-library-reference
ms.suite: pro-bi
ms.topic: conceptual
apiname:
- SecureConnectionLevel
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SecureConnectionLevel property
ms.assetid: fd5549e7-b874-41e2-866e-2f58caf6f733
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7d9132af7b33ff04fb17d8e74dd4edab06c1e0b3
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2018
ms.locfileid: "43278940"
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
 Un valor **Integer** que representa el nivel de conexión segura. Los valores devueltos indican que el SSL está configurado o no. Un valor mayor o igual que 1 indica que SSL está activado. El valor 0 indica que SSL está desactivado.  
  
## <a name="example-code"></a>Código de ejemplo  
 [Clase MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>Notas

En SQL Server 2008 R2, SecureConnectionLevel actúa como un conmutador de activación o desactivación. Para obtener más información, consulte [Método ConfigurationSetting - SetSecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setsecureconnectionlevel.md).

## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Ver también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
