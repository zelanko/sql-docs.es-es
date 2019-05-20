---
title: Método DeleteEncryptionKey (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- DeleteEncryptionKey (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- DeleteEncryptionKey method
ms.assetid: ed2f25b6-6a63-468d-9279-a577ca01b096
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e40c53c5c46d37a996805105563b809ad278b9a1
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/14/2019
ms.locfileid: "65570800"
---
# <a name="configurationsetting-method---deleteencryptionkey"></a>Método ConfigurationSetting - DeleteEncryptionKey
  Elimina las claves de cifrado de la base de datos del servidor de informes.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Sub DeleteEncryptionKeys(ByVal InstallationID As String, _  
    ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void DeleteEncryptionKeys(string InstallationID, out Int32 HRESULT,   
    out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>Parámetros  
 *InstallationID*  
 El identificador de instalación de un servidor de informes que está en la tabla de claves de la base de datos del servidor de informes.  
  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
 *ExtendedErrors[]*  
 [out] Matriz de cadenas que contiene los errores adicionales devueltos por la llamada.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve HRESULT que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente. Un valor distinto de cero indica que se ha producido un error.  
  
## <a name="remarks"></a>Notas  
 El método *DeleteEncryptionKey* elimina las entradas en la tabla de claves de todos los servidores de informes que tienen acceso a la información segura en la base de datos del servidor de informes. Si el parámetro *InstallationID* especificado no se corresponde con un identificador de instalación en la base de datos, el método devuelve un error.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
