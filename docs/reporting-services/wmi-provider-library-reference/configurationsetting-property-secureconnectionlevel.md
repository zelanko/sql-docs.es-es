---
title: Propiedad SecureConnectionLevel (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 42beaf5446038bfaa0faf1b8e95a4eb5fc6d16b8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47727903"
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
  
  
