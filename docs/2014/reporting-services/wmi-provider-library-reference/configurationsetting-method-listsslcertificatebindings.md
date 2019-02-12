---
title: Método ListSSLCertificateBindings (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- ListSSLCertificateBindings method
ms.assetid: d12d280c-9b6f-47a8-bcd9-34cde31c8886
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 9802176b5f5c82ba60a4e47d85445b54eaa1a5f0
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56031626"
---
# <a name="listsslcertificatebindings-method-wmi-msreportserverconfigurationsetting"></a>Método ListSSLCertificateBindings (WMI MSReportServer_ConfigurationSetting)
  Devuelve una lista de los certificados SSL instalados en el equipo.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Sub ListSSLCertificateBindings(ByVal LCID As Int32, ByRef Application() As String, _  
    ByRef CertificateHash() As String, ByRef IPAddresses() As String, ByRef Port() As Int32, _  
    ByRef Errors() As String, ByRef Length As Int32, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void ListSSLCertificateBindings(Int32 Lcid, out string[] Application,   
    out string[] CertificateHash,out string[] IPAddress,   
    out Int32[] Port, out string Errors,   
    out Int32 length, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parámetros  
 *LCID*  
 Configuración regional que se utilizará para los mensajes de error que se devuelven.  
  
 *Application[]*  
 [out] Aplicaciones que tienen enlaces de certificado.  
  
 *CertificateHash[]*  
 [out] Valores hash para los certificados.  
  
 *IPAddress[]*  
 [out] Dirección IP para las aplicaciones.  
  
 *Port[]*  
 [out] Número de puerto almacenado en el enlace en rsreportserver.config.  
  
 *Errors[]*  
 [out] Descripciones de los errores que se produjeron.  
  
 *Longitud*  
 [out] Longitud de la matriz devuelta por el método.  
  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente. Un valor distinto de cero indica que se ha producido un error.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
