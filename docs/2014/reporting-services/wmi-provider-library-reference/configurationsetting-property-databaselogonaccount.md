---
title: Propiedad DatabaseLogonAccount (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- DatabaseLogonAccount
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- DatabaseLogonAccount property
ms.assetid: 55f2863f-1ac1-4519-b512-e7f11c0ea5ea
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cfcfde7491252568ac8dc89b9ceb1da64c6497dc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66097893"
---
# <a name="databaselogonaccount-property-wmi-msreportserver_configurationsetting"></a>Propiedad DatabaseLogonAccount (WMI MSReportServer_ConfigurationSetting)
  Especifica la cuenta de inicio de sesión que el servidor de informes utiliza al conectarse a la base de datos del servidor de informes. Solo lectura.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Dim DatabaseLogonAccount As String  
```  
  
```csharp  
public string DatabaseLogonAccount;  
```  
  
## <a name="property-values"></a>Valores de propiedad  
 Un objeto `String` que representa el nombre de la cuenta de inicio de sesión.  
  
## <a name="example-code"></a>Código de ejemplo  
 [Clase MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>Observaciones  
 Los valores válidos para esta propiedad variarán dependiendo del valor de la propiedad [DatabaseLogonType](configurationsetting-property-databaselogontype.md) .  
  
 Esta propiedad se omite si la propiedad [DatabaseLogonType](configurationsetting-property-databaselogontype.md) está establecida en `2 (Service)`.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Miembros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
