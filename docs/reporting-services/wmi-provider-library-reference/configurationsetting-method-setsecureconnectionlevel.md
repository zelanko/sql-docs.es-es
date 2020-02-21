---
title: Método SetSecureConnectionLevel (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- SetSecureConnectionLevel (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetSecureConnectionLevel method
ms.assetid: 0fac7d5e-2670-4657-9439-331e7d93babb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5318d25ed1e6113e65f6e41d40add3ff0203856c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "65580998"
---
# <a name="configurationsetting-method---setsecureconnectionlevel"></a>Método ConfigurationSetting - SetSecureConnectionLevel
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
 *Level*  
 Un valor entero que representa un nivel de conexión segura.  
  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente. Un valor distinto de cero indica que se ha producido un error.  
  
## <a name="remarks"></a>Observaciones  
 Cuando se realiza una llamada, la propiedad SecureConnectionLevel del servidor de informes se establece en el valor especificado. El valor 0 indica que SSL está desactivado. Un valor mayor o igual que 1 indica que SSL está activado.  
  
-   Cuando se establece el valor, se cambia el elemento SecureConnectionLevel del archivo de configuración del servidor de informes y el elemento **URLRoot** en el archivo de configuración se establece para usar "https://" si el valor de *Level* es mayor o igual que 1, o bien "http://" si el valor de *Level* especificado es 0.  
  
 En [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], SecureConnectionLevel actúa como un conmutador de activación o desactivación (el valor predeterminado es 0). Para cualquier valor mayor o igual que 1 pasado a la API con el método SetSecureConnectionLevel, SSL se considera activado y la propiedad SecureConnectionLevel de configuración se establece en consecuencia en el archivo rsreportserver.config. Los valores 2 y 3 todavía se permiten por mantener la compatibilidad con las versiones anteriores.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
