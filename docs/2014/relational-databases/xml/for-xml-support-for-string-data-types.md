---
title: Compatibilidad con FOR XML para tipos de datos de cadena | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- strings [SQL Server], XML
ms.assetid: bf069da8-de1e-44d2-a1fb-ade383076ac1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77a061d9a4bc1b1e320cf8af01599cdc52e139f8
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58537467"
---
# <a name="for-xml-support-for-string-data-types"></a>Compatibilidad con FOR XML para tipos de datos de cadena
  Se crea una entidad del XML generado por los caracteres de espacio en blanco de FOR XML en los datos.  
  
 En el ejemplo siguiente se crea una tabla de ejemplo **T** y se insertan datos de ejemplo que incluyen los caracteres de avance de línea, retorno de carro y tabulación. La instrucción SELECT recupera los datos de la tabla.  
  
```  
CREATE TABLE T  
(  
  c1 int identity primary key,  
  c2 varchar(100)  
);  
go  
  
INSERT T (c2) VALUES ('Special character 0xD for carriage return ' + convert(varchar(10), 0xD) + ' after carriage return');  
INSERT T (c2) VALUES ('Special character 0x9 for tab ' + convert(varchar(10), 0x9) + ' after tab' );  
INSERT T (c2) VALUES ('Special character 0xA for line feed ' + convert(varchar(10), 0xA) + ' after line feed');  
go  
SELECT *   
FROM T  
FOR XML AUTO;  
go  
```  
  
 Éste es el resultado:  
  
```  
 <T c1="1" c2="Special character 0xD for carriage return   
 after carriage return" />  
 <T c1="2" c2="Special character 0x9 for tab     after tab" />  
 <T c1="3" c2="Special character 0xA for line feed   
after line feed" />  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   Se crea la entidad &#xD para el retorno de carro de la primera fila.  
  
-   Se crea la entidad &#x09 para el carácter de tabulación de la segunda fila.  
  
-   Se crea la entidad &#xA para el carácter de avance de línea de la tercera fila.  
  
## <a name="see-also"></a>Vea también  
 [Compatibilidad con FOR XML para varios tipos de datos de SQL Server](for-xml-support-for-various-sql-server-data-types.md)  
  
  
