---
title: "Elemento Banner (ssbdiagnose) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "banner, elemento"
  - "formato del archivo de salida XML [ssbdiagnose], elemento Banner"
  - "ssbdiagnose"
ms.assetid: cc6cd49a-acf0-4cfb-8c6a-554692b89de2
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# Elemento Banner (ssbdiagnose)
  Identifica la utilidad que generó el archivo de salida XML de **ssbdiagnose** .  
  
## Sintaxis  
  
```  
  
<Banner  
    title="..."   
    product="..."   
    version="..." />  
```  
  
## Atributos del elemento  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|**title**|Identifica la utilidad que generó el archivo de salida XML de **ssbdiagnose** .|  
|**product**|Identifica el producto que generó el archivo de salida XML de **ssbdiagnose** .|  
|**version**|Identifica la versión de la utilidad que generó el archivo de salida XML.|  
  
## Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Se produce una vez por archivo de salida XML de **ssbdiagnose** .|  
  
## Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Elemento DiagnosticInformation &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/diagnosticinformation-element-ssbdiagnose.md)|  
|**Elementos secundarios**|Ninguno.|  
  
## Ejemplo  
 Este es un ejemplo de un elemento banner.  
  
```  
<Banner title="Service Broker Diagnostics Utility" product="Microsoft SQL Server" version="10.0.1073.0" />  
```  
  
## Vea también  
 [utilidad ssbdiagnose &#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  