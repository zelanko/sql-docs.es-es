---
title: Usar la opción BINARY BASE64 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- AUTO FOR XML mode, BINARY BASE64 option
ms.assetid: 86a7bb85-7f83-412a-b775-d2c379702fe9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1bda0167e1e55c3ded715de96027a153ec5a65de
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63231254"
---
# <a name="use-the-binary-base64-option"></a>Usar la opción BINARY BASE64
  Si en la consulta se especifica la opción BINARY BASE64, los datos binarios se devuelven en formato de codificación en base64. De manera predeterminada, si no se especifica la opción BINARY BASE64, el modo AUTO admite la codificación URL de datos binarios. Es decir, en lugar de datos binarios, se devuelve una referencia a una dirección URL relativa a la raíz virtual de la base de datos donde se ejecutó la consulta. Esta referencia se puede utilizar para obtener acceso a los datos binarios reales en operaciones posteriores mediante la consulta dbobject SQLXML ISAPI. La consulta debe proporcionar suficiente información, como las columnas de clave principal, para identificar la imagen.  
  
 Al especificar una consulta, si se utiliza un alias para la columna binaria de la vista, se devuelve el alias en la codificación URL de los datos binarios. En operaciones posteriores, el alias no tiene ningún significado y no es posible utilizar la codificación de dirección URL para recuperar la imagen. Por consiguiente, no utilice alias si consulta una vista con el modo FOR XML AUTO.  
  
 Por ejemplo, en una consulta SELECT, la conversión de una columna en un objeto binario grande (BLOB) convierte a la columna en una entidad temporal en la que pierde su nombre asociado de tabla y de columna. Esto hace que las consultas en modo AUTO generen un error, ya que no sabe dónde colocar este valor en la jerarquía XML. Por ejemplo:  
  
```  
CREATE TABLE MyTable (Col1 int PRIMARY KEY, Col2 binary)  
INSERT INTO MyTable VALUES (1, 0x7);  
```  
  
 Esta consulta produce un error debido a la conversión en un objeto binario grande (BLOB):  
  
```  
SELECT Col1,  
CAST(Col2 as image) as Col2  
FROM MyTable  
FOR XML AUTO;  
```  
  
 La solución consiste en agregar la opción BINARY BASE64 a la cláusula FOR XML. Si se quita la conversión, la consulta produce los resultados esperados:  
  
```  
SELECT Col1,  
CAST(Col2 as image) as Col2  
FROM MyTable  
FOR XML AUTO, BINARY BASE64;  
```  
  
 Éste es el resultado:  
  
```  
<MyTable Col1="1" Col2="Bw==" />  
```  
  
## <a name="see-also"></a>Vea también  
 [Usar el modo AUTO con FOR XML](use-auto-mode-with-for-xml.md)  
  
  
