---
title: "Generar elementos para valores NULL mediante el par&#225;metro XSINIL | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "cláusula FOR XML, valores null"
  - "valores null [SQL Server], XML"
  - "ELEMENTS, directiva"
  - "XSINIL, parámetro"
ms.assetid: 2dbc4e48-1cae-4d83-b371-3265da9687cc
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# Generar elementos para valores NULL mediante el par&#225;metro XSINIL
  La directiva **ELEMENTS** genera XML en el cual cada valor de columna se asigna a un elemento del XML. Si el valor de la columna es NULL, no se agrega ningún elemento. Al especificar el parámetro **XSINIL** opcional en la directiva ELEMENTS, se puede solicitar que también se cree un elemento para el valor NULL. En este caso, se devuelve un elemento que tiene el atributo **xsi:nil** establecido en TRUE para cada valor de columna NULL.  
  
## Vea también  
 [Usar el modo RAW con FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
  
  