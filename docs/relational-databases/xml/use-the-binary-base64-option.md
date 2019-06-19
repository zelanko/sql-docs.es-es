---
title: Usar la opción BINARY BASE64 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- AUTO FOR XML mode, BINARY BASE64 option
ms.assetid: 86a7bb85-7f83-412a-b775-d2c379702fe9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 693a4d95d6c9eb3e290c1b39f8be9cc15c96bb13
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62704628"
---
# <a name="use-the-binary-base64-option"></a>Usar la opción BINARY BASE64
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
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
  
 El resultado es el siguiente:  
  
```  
<MyTable Col1="1" Col2="Bw==" />  
```  
  
## <a name="see-also"></a>Consulte también  
 [Usar el modo AUTO con FOR XML](../../relational-databases/xml/use-auto-mode-with-for-xml.md)  
  
  
