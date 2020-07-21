---
title: Generar XML a partir de conjuntos de filas con FOR XML | Microsoft Docs
description: Obtenga información sobre cómo generar una instancia de tipo de datos XML a partir de un conjunto de filas mediante la directiva TYPE con la cláusula FOR XML.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, generating XML from rowsets
ms.assetid: d061c0f1-3de9-4ad1-bbca-ce45d064b6c8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0a3db0a22d7bcba85d77979383c004f0834fe422
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85691243"
---
# <a name="generate-xml-from-rowsets-with-for-xml"></a>Generar XML a partir de conjuntos de filas con FOR XML
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Se puede generar una instancia de tipo de datos **xml** a partir de un conjunto de filas mediante FOR XML con la nueva directiva **TYPE** .  
  
 El resultado se puede asignar a una columna, una variable o un parámetro de tipo de datos **xml** . Además, FOR XML se puede anidar para generar una estructura jerárquica. Por ello, FOR XML anidado resulta mucho más cómodo de escribir que FOR XML EXPLICIT, aunque tal vez no funcione tan bien para jerarquías con muchos niveles. FOR XML también incorpora un nuevo modo PATH. Este nuevo modo especifica la ruta de acceso en el árbol XML donde aparece un valor de columna.  
  
 La nueva directiva **FOR XML TYPE** puede emplearse para definir vistas XML de solo lectura en datos relacionales con sintaxis SQL. Es posible realizar consultas en la vista con instrucciones SQL y XQuery incrustado, como se indica en el ejemplo siguiente. También se puede hacer referencia a estas vistas SQL en procedimientos almacenados.  
  
## <a name="example-sql-view-returning-generated-xml-data-type"></a>Ejemplo: Vista SQL que devuelve el tipo de datos XML generado  
 La siguiente definición de vista SQL crea una vista XML de una columna relacional, pk, y de los autores de libros recuperados de una columna XML:  
  
```  
CREATE VIEW V (xmlVal) AS  
SELECT pk, xCol.query('/book/author')  
FROM   T  
FOR XML AUTO, TYPE  
```  
  
 La vista V contiene una sola fila y una sola columna xmlVal de tipo XML`.` Se puede consultar como una instancia de tipo de datos **xml** normal. Por ejemplo, la siguiente consulta devuelve el autor cuyo nombre es "David":  
  
```  
SELECT xmlVal.query('//author[first-name = "David"]')  
FROM   V  
```  
  
 Las definiciones de vistas SQL son en cierto modo similares a las vistas XML que se crean mediante esquemas anotados. Sin embargo, hay tres diferencias importantes. La definición de vista SQL es de solo lectura y se debe manipular con XQuery incrustado. Las vistas XML se crean mediante un esquema anotado. Además, la vista SQL materializa el resultado XML antes de aplicar la expresión XQuery, mientras que las consultas XPath en las vistas XML evalúan consultas SQL en las tablas subyacentes.  
  
## <a name="see-also"></a>Consulte también  
 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
