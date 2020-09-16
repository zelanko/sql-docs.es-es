---
description: Método SetUnattendedExecutionAccount (WMI MSReportServer_ConfigurationSetting)
title: Método SetUnattendedExecutionAccount ( MSeportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- SetUnattendedExecutionAccount (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetUnattendedExecutionAccount method
ms.assetid: 1ba6be6f-b05c-4ea0-af98-cd0780290b70
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5f65c36ae1f27039061642dba87ec79b6f81c7c2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497928"
---
# <a name="configurationsetting-method---setunattendedexecutionaccount"></a>Método ConfigurationSetting - SetUnattendedExecutionAccount
  Especifica la cuenta utilizada para ejecutar informes de forma desatendida.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Sub SetUnattendedExecutionAccount(UserName as String, _  
    Password as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void SetUnattendedExecutionAccount (string UserName,   
    string Password, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parámetros  
 *UserName*  
 Una cuenta de Windows que se utilizará para las ejecuciones desatendidas.  
  
 *Contraseña*  
 La contraseña de la cuenta especificada.  
  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente. Un valor distinto de cero indica que se ha producido un error.  
  
## <a name="remarks"></a>Observaciones  
 El método SetUnattendedExecutionAccount no comprueba si el servidor de informes puede iniciar sesión como el usuario especificado.  
  
 No se puede usar el método SetUnattendedExecutionAccount para las ejecuciones desatendidas en el contexto del servicio Servidor de informes de Windows.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
