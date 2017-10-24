---
title: Banner de elemento (ssbdiagnose) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- banner element
- XML output file format [ssbdiagnose], banner element
- ssbdiagnose
ms.assetid: cc6cd49a-acf0-4cfb-8c6a-554692b89de2
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0b203f5c2f9700137409df074935c2f17daf08d7
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="banner-element-ssbdiagnose"></a>Elemento Banner (ssbdiagnose)
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
|**Elemento primario**|[Elemento DiagnosticInformation &#40; ssbdiagnose &#41;](../../tools/ssbdiagnose/diagnosticinformation-element-ssbdiagnose.md)|  
|**Elementos secundarios**|Ninguno.|  
  
## <a name="example"></a>Ejemplo  
 Este es un ejemplo de un elemento banner.  
  
```  
<Banner title="Service Broker Diagnostics Utility" product="Microsoft SQL Server" version="10.0.1073.0" />  
```  
  
## <a name="see-also"></a>Vea también  
 [Utilidad ssbdiagnose &#40; Service Broker &#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  

