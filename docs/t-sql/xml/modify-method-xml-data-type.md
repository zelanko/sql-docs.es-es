---
title: Modify() (método del tipo de datos xml) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
manager: craigg
ms.openlocfilehash: ca8c4e82cbe4788b7eb3fda179daa4e6c63fe70e
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36258396"
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
  
  
