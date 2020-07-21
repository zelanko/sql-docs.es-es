---
title: Elemento Banner
diagnose: In SQL Server, the Banner element identifies which utility generated the ssbdiagnose output XML file.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- banner element
- XML output file format [ssbdiagnose], banner element
- ssbdiagnose
ms.assetid: cc6cd49a-acf0-4cfb-8c6a-554692b89de2
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 8b8e112c3d83704870c43f2971b2774ffd9b6b34
ms.sourcegitcommit: b8933ce09d0e631d1183a84d2c2ad3dfd0602180
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/13/2020
ms.locfileid: "83150541"
---
# <a name="banner-element-ssbdiagnose"></a>Elemento Banner (ssbdiagnose)


[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Identifica la utilidad que generó el archivo de salida XML de **ssbdiagnose** .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Banner  
    title="..."   
    product="..."   
    version="..." />  
```  
  
## <a name="element-attributes"></a>Atributos del elemento  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|**title**|Identifica la utilidad que generó el archivo de salida XML de **ssbdiagnose** .|  
|**product**|Identifica el producto que generó el archivo de salida XML de **ssbdiagnose** .|  
|**version**|Identifica la versión de la utilidad que generó el archivo de salida XML.|  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Se produce una vez por archivo de salida XML de **ssbdiagnose** .|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Elemento DiagnosticInformation &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/diagnosticinformation-element-ssbdiagnose.md)|  
|**Elementos secundarios**|Ninguno.|  
  
## <a name="example"></a>Ejemplo  
 Este es un ejemplo de un elemento banner.  
  
```  
<Banner title="Service Broker Diagnostics Utility" product="Microsoft SQL Server" version="10.0.1073.0" />  
```  
  
## <a name="see-also"></a>Consulte también  
 [Utilidad ssbdiagnose &#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  
