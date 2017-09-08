---
title: "Modify() (método) (tipo de datos xml) | Documentos de Microsoft"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- modify() method
- modify method
ms.assetid: 52430735-51f4-46d1-a308-9aecf8648fda
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 81838bf62f9b2c92dce4df8a167785fdfbf7abb2
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="modify-method-xml-data-type"></a>Modify() (método del tipo de datos xml)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Modifica el contenido de un documento XML. Utilice este método para modificar el contenido de un **xml** columna o variable de tipo. Este método toma una instrucción XML DML para insertar, actualizar o eliminar nodos a partir de datos XML. El **modify()** método de la **xml** tipo de datos solo puede usarse en la cláusula SET de una instrucción UPDATE.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
modify (XML_DML)  
```  
  
## <a name="arguments"></a>Argumentos  
 XML_DML  
 Es una cadena en lenguaje de manipulación de datos (DML) XML. El documento XML se actualiza conforme a esta expresión.  
  
> [!NOTE]  
>  Se devuelve un error si la **modify()** método se llama en un valor null o da como resultado un valor null.  
  
## <a name="examples"></a>Ejemplos  
 Dado que la **modify()** método requiere una cadena en el XML datos lenguaje de manipulación (DML), los ejemplos de **modify()** se encuentran en los temas que describen las instrucciones XML DML. Para estos ejemplos, vea [insert &#40; XML DML &#41; ](../../t-sql/xml/insert-xml-dml.md), [delete &#40; XML DML &#41; ](../../t-sql/xml/delete-xml-dml.md) y [reemplazar el valor de &#40; XML DML &#41; ](../../t-sql/xml/replace-value-of-xml-dml.md).  
  
## <a name="see-also"></a>Vea también  
 [Crear instancias de datos XML](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [métodos del tipo de datos xml](../../t-sql/xml/xml-data-type-methods.md)   
 [Lenguaje de manipulación de datos XML &#40; XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  

