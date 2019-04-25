---
title: Propiedad IsSharePointIntegrated (WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- IsSharePointIntegrated property
ms.assetid: c548fed8-5e04-4faf-8b10-b37c86178056
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 08f27657e4ba0e586c5734d2575b5017e8bfc1ac
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62645919"
---
# <a name="issharepointintegrated-property-wmi"></a>Propiedad IsSharePointIntegrated (WMI)
  Especifica si el servidor de informes está en modo integrado de SharePoint. A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], esta propiedad siempre devuelve `False`, porque en modo de SharePoint las instancias de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] son servicios compartidos de SharePoint y los proveedores WMI no las controlan.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Dim IsSharePointIntegrated As Boolean  
```  
  
```csharp  
public Boolean IsSharePointIntegrated;  
```  
  
## <a name="property-values"></a>Valores de propiedad  
 Un objeto `Boolean` que indica si el servidor de informes está en modo integrado de SharePoint.  
  
## <a name="example-code"></a>Código de ejemplo  
 [Clase MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
