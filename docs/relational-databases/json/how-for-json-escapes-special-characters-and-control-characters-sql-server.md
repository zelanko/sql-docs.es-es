---
title: "C&#243;mo FOR JSON inserta caracteres de escape en los caracteres especiales y caracteres de control (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FOR JSON, caracteres especiales"
ms.assetid: 4ba90025-5a09-4f0a-836a-54c886324530
caps.latest.revision: 16
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# C&#243;mo FOR JSON inserta caracteres de escape en los caracteres especiales y caracteres de control (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  En este tema se describe cómo la cláusula **FOR JSON** inserta caracteres de escape en los caracteres especiales y representa caracteres de control en la salida JSON.  
  
## Secuencia de caracteres de escape en los caracteres especiales  
 La cláusula **FOR JSON** inserta caracteres de escape en los caracteres especiales del resultado JSON con `\`, como se muestra en la tabla siguiente. Esta secuencia de escape se produce tanto en los nombres de propiedades como en sus valores.  
  
|**Carácter especial**|**Secuencia codificada**|  
|---------------------------|--------------------------|  
|Comillas (")|\\"|  
|Barra diagonal inversa (\\)|\\\|  
|Barra diagonal (/)|\\/|  
|Retroceso|\b|  
|Avance de página|\f|  
|Nueva línea|\n|  
|Retorno de carro|\r|  
|Tabulación horizontal|\t|  
  
## Caracteres de control  
 La cláusula **FOR JSON** representa los caracteres de control de la salida JSON en formato `\u<code>`, como se muestra en la tabla siguiente.  
  
|**Carácter de control**|**Secuencia codificada**|  
|---------------------------|--------------------------|  
|CHAR(0)|\u0000|  
|CHAR(1)|\u0001|  
|…|…|  
|CHAR(31)|\u001f|  
  
## Ejemplo  
 Este es un ejemplo de una cláusula **FOR JSON** que incluye caracteres de escape y de control.  
  
 Consulta:  
  
```tsql  
SELECT  
  'VALUE\    /  
  "' as [KEY\/"],  
  CHAR(0) as '0',  
  CHAR(1) as '1',  
  CHAR(31) as '31'  
FOR JSON PATH  
```  
  
 Resultado:  
  
```json  
{  
   "KEY\\\t\/\"":"VALUE\\\t\/\r\n\"",  
   "0":"\u0000",  
   "1":"\u0001",  
  "31":"\u001f“  
}  
```  
  
## Vea también  
 [Format Query Results as JSON with FOR JSON &#40;SQL Server&#41; (Dar formato JSON a los resultados de consulta con FOR JSON &#40;SQL Server&#41;)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  