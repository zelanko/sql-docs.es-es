---
title: Método ListSSLCertificateBindings (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
helpviewer_keywords:
- ListSSLCertificateBindings method
ms.assetid: d12d280c-9b6f-47a8-bcd9-34cde31c8886
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9fccf663b91dfba2c7b68da1c882c6c6f701e42f
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/17/2020
ms.locfileid: "81636195"
---
# <a name="configurationsetting-method---listsslcertificatebindings"></a>Método ConfigurationSetting - ListSSLCertificateBindings
  Devuelve una lista de los certificados TLS/SSL instalados en el equipo.  
  
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
  
## <a name="remarks"></a>Observaciones  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
