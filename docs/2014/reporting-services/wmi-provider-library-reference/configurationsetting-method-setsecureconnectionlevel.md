---
title: Método SetSecureConnectionLevel (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
api_name:
- SetSecureConnectionLevel (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetSecureConnectionLevel method
ms.assetid: 0fac7d5e-2670-4657-9439-331e7d93babb
caps.latest.revision: 21
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 5af02be1c79b69fa113bec095ea9bf7a35354799
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37185778"
---
# <a name="setsecureconnectionlevel-method-wmi-msreportserverconfigurationsetting"></a>Método SetSecureConnectionLevel (WMI MSReportServer_ConfigurationSetting)
  Establece el nivel de conexión segura del servidor de informes.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Sub SetSecureConnectionLevel(Level as Integer, _  
    ByRef HRESULT as Int32)  
```  
  
```csharp  
public void SetSecureConnectionLevel(Int32 Level,   
    out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parámetros  
 *Nivel*  
 Un valor entero que representa un nivel de conexión segura.  
  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente. Un valor distinto de cero indica que se ha producido un error.  
  
## <a name="remarks"></a>Notas  
 Cuando se realiza una llamada, la propiedad SecureConnectionLevel del servidor de informes se establece en el valor especificado. El valor 0 indica que SSL está desactivado. Un valor mayor o igual que 1 indica que SSL está activado.  
  
-   Cuando se establece el valor, se cambia el elemento SecureConnectionLevel en el archivo de configuración del servidor de informes y el `URLRoot` en el archivo de configuración está establecida para utilizar "https://" si especificado *nivel* es mayor que o igual que 1 o "http://" si especificado *nivel* es 0.  
  
 En [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], SecureConnectionLevel actúa como un conmutador de activación o desactivación (el valor predeterminado es 0). Para cualquier valor mayor o igual que 1 pasado a la API con el método SetSecureConnectionLevel, SSL se considera activado y la propiedad SecureConnectionLevel de configuración se establece en consecuencia en el archivo rsreportserver.config. Los valores 2 y 3 todavía se permiten por mantener la compatibilidad con las versiones anteriores.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
