---
title: Método SetEmailConfiguration (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- SetEmailConfiguration (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetEmailConfiguration method
ms.assetid: b40a2224-2c90-4d32-892f-1fe73a0591ca
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 227122568d206e9459811b090b1b1dbb2c53c356
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47756304"
---
# <a name="configurationsetting-method---setemailconfiguration"></a>Método ConfigurationSetting - SetEmailConfiguration
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
  
## <a name="remarks"></a>Notas  
 Cuando el parámetro *SendUsingSMTPServer* se establece en **true**, la entrada de **SendUsing** en el archivo de configuración del servidor de informes se establece en 1. Cuando *SendUsingSMTPServer* se establece en **false**, la entrada de **SendUsing** no se configura.  
  
 Este método no proporciona una manera para que los usuarios establezcan la entrada de **SendUsing** en el archivo de configuración del servidor de informes en un valor distinto de 1. Para configurar el servidor de informes para algo distinto del correo SMTP, debe modificar manualmente el archivo de configuración.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Ver también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
