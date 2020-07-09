---
title: Modify() (método del tipo de datos xml) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- modify() method
- modify method
ms.assetid: 52430735-51f4-46d1-a308-9aecf8648fda
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7182961996510fcded86a3e1d218d482eb834e63
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85731060"
---
# <a name="modify-method-xml-data-type"></a>Modify() (método del tipo de datos xml)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

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
  
## <a name="see-also"></a>Consulte también  
 [Crear instancias de datos XML](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [métodos del tipo de datos xml](../../t-sql/xml/xml-data-type-methods.md)   
 [Lenguaje de manipulación de datos XML &#40;XML DML&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
