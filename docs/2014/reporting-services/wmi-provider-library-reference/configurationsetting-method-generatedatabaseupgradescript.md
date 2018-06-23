---
title: Método GenerateDatabaseUpgradeScript (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
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
- GenerateDatabaseUpgradeScript (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- GenerateDatabaseUpgradeScript method
ms.assetid: 88534e8e-2877-41cd-b5c2-b1d33a0fd203
caps.latest.revision: 22
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: cc2a4795b9549ef3a39de971ac07ab1282d26990
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103468"
---
# <a name="generatedatabaseupgradescript-method-wmi-msreportserverconfigurationsetting"></a>Método GenerateDatabaseUpgradeScript (WMI MSReportServer_ConfigurationSetting)
  Genera un script que se puede utilizar para actualizar la base de datos del servidor de informes al esquema de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] .  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Sub GenerateDatabaseUpgradeScript(DatabaseName as String, _  
    ServerVersion as String, ByRef Script as String, _  
    ByRef HRESULT as Int32)  
```  
  
```csharp  
public void GenerateDatabaseUpgradeScript (string DatabaseName,   
    string ServerVersion, out string Script,   
    out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parámetros  
 *Databasename*  
 Cadena que contiene el nombre de la base de datos del servidor de informes que se va a actualizar.  
  
 *ServerVersion*  
 Cadena que contiene la versión del servidor de informes.  
  
 *Script*  
 [out] Cadena que contiene el script SQL generado.  
  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente. Un valor distinto de cero indica que se ha producido un error.  
  
## <a name="remarks"></a>Notas  
 El script generado admite [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]y [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  