---
title: Propiedad DatabaseLogonAccount (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- DatabaseLogonAccount
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- DatabaseLogonAccount property
ms.assetid: 55f2863f-1ac1-4519-b512-e7f11c0ea5ea
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 603ae515642fa524841c160cafc82c4e8ace3249
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/14/2019
ms.locfileid: "65571654"
---
# <a name="configurationsetting-property---databaselogonaccount"></a>Propiedad ConfigurationSetting - DatabaseLogonAccount
  Especifica la cuenta de inicio de sesión que el servidor de informes utiliza al conectarse a la base de datos del servidor de informes. Solo lectura.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Dim DatabaseLogonAccount As String  
```  
  
```csharp  
public string DatabaseLogonAccount;  
```  
  
## <a name="property-values"></a>Valores de propiedad  
 Un objeto **String** que representa el nombre de la cuenta de inicio de sesión.  
  
## <a name="example-code"></a>Código de ejemplo  
 [Clase MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>Notas  
 Los valores válidos para esta propiedad variarán dependiendo del valor de la propiedad [DatabaseLogonType](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontype.md) .  
  
 Esta propiedad se omite si la propiedad [DatabaseLogonType](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontype.md) se ha establecido como **2 (Service)**.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
