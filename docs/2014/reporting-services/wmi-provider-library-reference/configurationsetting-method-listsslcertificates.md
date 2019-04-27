---
title: Método ListSSLCertificates (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- ListSSLCertificates method
ms.assetid: 88cd0936-b202-4ab8-90f2-d9c3f66d37f4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: adda71c5ee0a88eabd619280457421bbf5ec0a75
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62646733"
---
# <a name="listsslcertificates-method-wmi-msreportserverconfigurationsetting"></a>Método ListSSLCertificates (WMI MSReportServer_ConfigurationSetting)
  Devuelve una lista de certificados en el equipo del servidor de informes.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Sub CreateSSLCertificateBinding (ByRef CertificateHash() as String, _  
    ByRef CertName() as String, ByRef HostName() as String, ByRef Length as Int32, _   
    ByRef HRESULT as Int32)  
```  
  
```csharp  
public void ListSSLCertificates(out string[] CertificateHash,   
    out string[] CertName, out string[] Hostname, out Int32 length,   
    out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parámetros  
 *CertificateHash[]*  
 [out] Valores hash del certificado.  
  
 *CertName[]*  
 [out] Nombres del certificado.  
  
 *HostName[]*  
 [out] Nombres de host para los certificados.  
  
 *Longitud*  
 [out] Representa la longitud de las matrices *CertificateHash*, *CertName* y *HostName* .  
  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente; un código de error indica que la llamada no se realizó correctamente.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
