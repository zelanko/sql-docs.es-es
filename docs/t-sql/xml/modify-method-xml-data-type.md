---
title: "Modify() (método del tipo de datos xml) | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 429797447e56ecb57f0dc257bfd13bea59ea1f40
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="modify-method-xml-data-type"></a>Modify() (método del tipo de datos xml)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Modifica el contenido de un documento XML. Use este método para modificar el contenido de una columna o variable de tipo **xml**. Este método toma una instrucción XML DML para insertar, actualizar o eliminar nodos a partir de datos XML. El método **modify()** del tipo de datos **xml** solo se puede usar en la cláusula SET de una instrucción UPDATE.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
modify (XML_DML)  
```  
  
## <a name="arguments"></a>Argumentos  
 XML_DML  
 Es una cadena en lenguaje de manipulación de datos (DML) XML. El documento XML se actualiza conforme a esta expresión.  
  
> [!NOTE]  
>  Se devuelve un error si se llama al método **modify()** sobre un valor NULL o da como resultado un valor NULL.  
  
## <a name="examples"></a>Ejemplos  
 Puesto que el método **modify()** requiere una cadena en el lenguaje de manipulación de datos (DML) XML, los ejemplos de **modify()** se encuentran en los temas que tratan sobre las instrucciones XML DML. Para obtener estos ejemplos, vea [insert &#40;XML DML&#41;](../../t-sql/xml/insert-xml-dml.md), [delete &#40;XML DML&#41;](../../t-sql/xml/delete-xml-dml.md) y [replace value of &#40;XML DML&#41;](../../t-sql/xml/replace-value-of-xml-dml.md).  
  
## <a name="see-also"></a>Ver también  
 [Crear instancias de datos XML](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [métodos del tipo de datos xml](../../t-sql/xml/xml-data-type-methods.md)   
 [Lenguaje de manipulación de datos XML &#40;XML DML&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
