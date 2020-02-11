---
title: Modificación de índices XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XML indexes [SQL Server], modifying
- modifying indexes
ms.assetid: 24d50fe1-c6ec-49e6-91a3-9791851ba53d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 67767ae7ec3bda62783281385333fef89481f45d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68195598"
---
# <a name="modify-xml-indexes"></a>Modificar índices XML
  La instrucción DDL [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql) de [!INCLUDE[tsql](../../includes/tsql-md.md)] se puede usar para modificar índices XML y no XML existentes. No obstante, no todas las opciones ALTER INDEX están disponibles para índices XML. Las siguientes opciones no son válidas al modificar índices XML:  
  
-   La opción de reconstrucción y configuración IGNORE_DUP_KEY no es válida para índices XML. La opción de reconstrucción ONLINE debe establecerse en OFF para los índices XML secundarios. La opción DROP_EXISTING no se admite en la instrucción ALTER INDEX.  
  
-   Las modificaciones de la restricción de clave principal en la tabla de usuario no se propagan automáticamente a los índices XML. El usuario debe quitar los índices XML primero y volver a crearlos después.  
  
-   Cuando se especifica ALTER INDEX ALL, se aplica tanto a los índices XML como a los que no lo son. Se pueden especificar opciones de indización que no sean válidas para ambos tipos de índices. En este caso, la instrucción producirá un error.  
  
## <a name="example-modifying-an-xml-index"></a>Ejemplo: Modificar un índice XML  
 En el ejemplo siguiente se muestra cómo crear un índice XML y, a continuación, modificarlo estableciendo la opción `ALLOW_ROW_LOCKS` en `OFF`. Cuando `ALLOW_ROW_LOCKS` se ha establecido en `OFF`, las filas no se bloquean y el acceso a los índices especificados se obtiene usando los bloqueos de página y de tabla.  
  
```  
CREATE TABLE T (Col1 INT PRIMARY KEY, XmlCol XML)  
GO  
-- Create primary XML index.   
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlCol)  
GO  
-- Note the type 3 is index on XML type.  
SELECT *  
FROM sys.xml_indexes  
WHERE object_id = object_id('T')  
AND name='PIdx_T_XmlCol'  
  
-- Modify and set an index option.  
ALTER INDEX PIdx_T_XmlCol on T   
SET (ALLOW_ROW_LOCKS = OFF)  
```  
  
## <a name="example-disabling-and-enabling-an-xml-index"></a>Ejemplo: Deshabilitar y habilitar un índice XML  
 Un índice XML está habilitado de forma predeterminada. Si un índice XML se deshabilita, las consultas que se realicen en la columna XML no usarán el índice XML. Para habilitar un índice XML, use `ALTER INDEX` con la opción `REBUILD` .  
  
```  
CREATE TABLE T (Col1 INT PRIMARY KEY, XmlCol XML)  
GO  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol ON T(XmlCol)  
GO  
ALTER INDEX PIdx_T_XmlCol on T DISABLE  
Go  
-- Verify index is disabled.  
SELECT *  
FROM sys.xml_indexes  
WHERE object_id = object_id('T')  
AND name='PIdx_T_XmlCol'  
-- Rebuild the index.  
ALTER INDEX PIdx_T_XmlCol on T REBUILD  
Go  
```  
  
## <a name="see-also"></a>Consulte también  
 [Índices XML &#40;SQL Server&#41;](xml-indexes-sql-server.md)  
  
  
