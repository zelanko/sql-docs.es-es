---
title: "Ejemplo: Especificar un elemento ra&#237;z para el XML generado por FOR XML | Microsoft Docs"
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
  - "modo RAW, ejemplo de especificar el elemento raíz"
  - "modo RAW, ejemplo con FOR XML"
ms.assetid: bcc54b11-0713-4e43-8dbe-d6f3ad1993b5
caps.latest.revision: 10
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 10
---
# Ejemplo: Especificar un elemento ra&#237;z para el XML generado por FOR XML
  Al especificar la opción `ROOT` en la consulta `FOR XML`, puede solicitar un solo elemento de nivel superior para el XML resultante, como se muestra en esta consulta. El argumento especificado para la directiva `ROOT` proporciona el nombre del elemento raíz.  
  
## Ejemplo  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name   
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119 or ProductModelID=115  
FOR XML RAW, ROOT('MyRoot')  
go  
```  
  
 El resultado es el siguiente:  
  
```  
<MyRoot>  
  <row ProductModelID="122" Name="All-Purpose Bike Stand" />  
  <row ProductModelID="119" Name="Bike Wash" />  
  <row ProductModelID="115" Name="Cable Lock" />  
</MyRoot>  
```  
  
## Vea también  
 [Usar el modo RAW con FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
  
  