---
title: Método SetWindowsServiceIdentity (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
api_name:
- SetWindowsServiceIdentity (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetWindowsServiceIdentity method
ms.assetid: 9bbc734c-9e69-48c2-8bec-8abe7c6cc987
caps.latest.revision: 19
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: fc3dfeafab01480fde7eb195363f46946de30ddd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196370"
---
# <a name="setwindowsserviceidentity-method-wmi-msreportserverconfigurationsetting"></a>Método SetWindowsServiceIdentity (WMI MSReportServer_ConfigurationSetting)
  Ejecuta el servicio de Windows de servidor de informes como el usuario de Windows especificado y concede a esta cuenta suficientes permisos de sistema de archivos para permitir que servidor de informes funcione.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Sub SetWindowsServiceIdentity(UseBuiltInAccount as Boolean, _  
    Account as String, Password as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void SetWindowsServiceIdentity(boolean UseBuiltInAccount,   
    string Account, string Password, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parámetros  
 *UseBuiltInAccount*  
 Indica si la cuenta especificada es una cuenta de Windows integrada.  
  
 *Cuenta*  
 La cuenta de Windows que se utilizará para ejecutar el servicio de Windows, en formato "DOMAIN\alias."  
  
 *Contraseña*  
 La contraseña de la cuenta.  
  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente. Un valor distinto de cero indica que se ha producido un error.  
  
## <a name="remarks"></a>Notas  
 Cuando el *UseBuiltInAccount* parámetro está establecido en `true` y se está ejecutando el servidor de informes en Microsoft [!INCLUDE[win2kfamily](../../includes/win2kfamily-md.md)] o Windows XP, el valor de la *nombre*, *dedominio*, y *contraseña* se omiten los parámetros y se utiliza la cuenta de sistema Local.  
  
 Cuando el *UseBuiltInAccount* parámetro está establecido en `true` y el servidor de informes se está ejecutando en Windows Server 2003, el *dominio* y *contraseña* propiedades son pasar por alto, y el campo de nombre debe contener "Builtin\NetworkService" o "Builtin\System" o "Builtin\LocalService".  
  
 El método SetWindowsServiceIdentity establece los permisos de archivo en los archivos y carpetas en el directorio de instalación del servidor de informes.  
  
 La cuenta especificada en el *cuenta* parámetro requiere `LogonAsService` derechos en Windows. El método permite este derecho a la cuenta especificada.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  