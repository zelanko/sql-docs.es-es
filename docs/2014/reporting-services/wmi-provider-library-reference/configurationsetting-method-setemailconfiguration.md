---
title: Método SetEmailConfiguration (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- SetEmailConfiguration (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetEmailConfiguration method
ms.assetid: b40a2224-2c90-4d32-892f-1fe73a0591ca
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 142fd8bf2116d4cc672aeb607938ea8c1c73bf8a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66097984"
---
# <a name="setemailconfiguration-method-wmi-msreportserverconfigurationsetting"></a>Método SetEmailConfiguration (WMI MSReportServer_ConfigurationSetting)
  Configura la extensión de entrega de correo electrónico utilizada por el servidor de informes para enviar el correo electrónico.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Sub SetEmailConfiguration(ByVal SendUsingSMTPServer As Boolean, _  
    ByVal SMTPServer As String, ByVal SenderEmailAddress As String, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetEmailConfiguration (Boolean SendUsingSMTPServer,   
   string SMTPServer, string SenderEmailAddress,   
   out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parámetros  
 *SendUsingSMTPServer*  
 Valor booleano que indica si el servidor utilizará el servidor SMTP para enviar el correo electrónico. Este valor solamente se puede establecer en true. El valor predeterminado es false.  
  
 *SMTPServer*  
 Cadena que contiene el nombre o dirección IP de un servidor SMTP.  
  
 *SenderEmailAddress*  
 Dirección de correo electrónico utilizada en el campo 'De:' para los correos electrónicos enviados desde el servidor de informes.  
  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente. Un valor distinto de cero indica que se ha producido un error.  
  
## <a name="remarks"></a>Comentarios  
 Cuando el *SendUsingSMTPServer* parámetro está establecido en `true`, **SendUsing** entrada en el archivo de configuración del servidor de informes está establecido en 1. Cuando *SendUsingSMTPServer* está establecido en `false`, **SendUsing** entrada no está configurada.  
  
 Este método no proporciona una manera para que los usuarios establezcan la entrada de **SendUsing** en el archivo de configuración del servidor de informes en un valor distinto de 1. Para configurar el servidor de informes para algo distinto del correo SMTP, debe modificar manualmente el archivo de configuración.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
