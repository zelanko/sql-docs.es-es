---
title: "Representar instant&#225;neas del historial de informes mediante acceso URL | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "acceso URL [Reporting Services], historial de informes"
  - "instantáneas de historial [Reporting Services]"
  - "datos históricos [Reporting Services]"
  - "instantáneas [Reporting Services], acceso URL"
  - "instantáneas [Reporting Services], representar historial de informes"
ms.assetid: 3f87f82d-0e61-4492-9c4b-f5238c39e8cd
caps.latest.revision: 32
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 32
---
# Representar instant&#225;neas del historial de informes mediante acceso URL
  Puede representar un informe basado en una instantánea del historial de informes si proporciona el parámetro *rs:Snapshot* y establece su valor en un identificador de instantánea válido. El valor del parámetro está en el formato AAAA-MM-DDTHH:MM:SS, según el estándar 8601 de la Organización internacional de normalización (ISO).  
  
 Si omite este parámetro, el informe se representa según la configuración de la ejecución del informe y de la administración de la memoria caché del servidor de informes. Para obtener más información sobre la ejecución del informe, vea [Establecer las propiedades del procesamiento de informes](../reporting-services/report-server/set-report-processing-properties.md).  
  
## Ejemplo  
 En el ejemplo siguiente se muestra una dirección URL que recupera una instantánea del historial de informes:  
  
```  
http://myrshost/reportserver?/SampleReports/Company Sales&rs:Snapshot=2003-04-07T13:40:02  
```  
  
## Vea también  
 [Acceso URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [Referencia de parámetros de acceso URL](../reporting-services/url-access-parameter-reference.md)  
  
  