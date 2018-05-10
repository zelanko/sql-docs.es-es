---
title: Método RemoveSSLCertificateBindings (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: wmi-provider-library-reference
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RemoveSSLCertificateBindings method
ms.assetid: b8b484c9-04c4-4ae9-980e-67bbe5aa8481
caps.latest.revision: 12
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 1ace3a19b111f92c62e64f3cdd015075d30ed0b0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="configurationsetting-method---removesslcertificatebinding"></a>Método ConfigurationSetting - RemoveSSLCertificateBinding
  Quita un enlace de certificado SSL.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Sub RemoveSSLCertificateBinding(ByVal Application As String, _  
    ByVal CertificateHash As String, ByVal IPAddress As String, _  
    ByVal Port As Int32, ByVal Lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void RemoveSSLCertificateBindings(string Application,  
    string CertificateHash, string IPAddress, Int32 Port, Int32 Lcid,  
    out string Error, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parámetros  
 *Aplicación*  
 El nombre de la aplicación para la que se debería quitar el enlace de certificado.  
  
 *CertificateHash*  
 Valor hash del certificado.  
  
 *IPAddress*  
 Dirección IP para la aplicación.  
  
 *Puerto*  
 Puerto SSL asociado al enlace.  
  
 *lcid*  
 Configuración regional que se utilizará para los mensajes de error que se devuelven.  
  
 *Error*  
 [out] Descripción del error que se produjo.  
  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente; un código de error indica que la llamada no se realizó correctamente.  
  
## <a name="remarks"></a>Notas  
 Este método quita el enlace específico del archivo rsreportserver.config y opcionalmente HTTP.SYS.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Ver también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
