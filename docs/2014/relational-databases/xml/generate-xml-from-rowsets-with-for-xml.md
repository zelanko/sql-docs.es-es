---
title: Generar XML a partir de conjuntos de filas con FOR XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, generating XML from rowsets
ms.assetid: d061c0f1-3de9-4ad1-bbca-ce45d064b6c8
author: rothja
ms.author: jroth
ms.openlocfilehash: 890c22e5ed4bd1414ba9454da293de0ddf6f595c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85046694"
---
# <a name="generate-xml-from-rowsets-with-for-xml"></a>Generar XML a partir de conjuntos de filas con FOR XML
  Puede generar una `xml` instancia de tipo de datos a partir de un conjunto de filas mediante for XML con la nueva directiva **Type** .  
  
 El resultado se puede asignar a una `xml` columna, variable o parámetro de tipo de datos. Además, FOR XML se puede anidar para generar una estructura jerárquica. Por ello, FOR XML anidado resulta mucho más cómodo de escribir que FOR XML EXPLICIT, aunque tal vez no funcione tan bien para jerarquías con muchos niveles. FOR XML también incorpora un nuevo modo PATH. Este nuevo modo especifica la ruta de acceso en el árbol XML donde aparece un valor de columna.  
  
 La nueva directiva **FOR XML TYPE** puede emplearse para definir vistas XML de solo lectura en datos relacionales con sintaxis SQL. Es posible realizar consultas en la vista con instrucciones SQL y XQuery incrustado, como se indica en el ejemplo siguiente. También se puede hacer referencia a estas vistas SQL en procedimientos almacenados.  
  
## <a name="example-sql-view-returning-generated-xml-data-type"></a>Ejemplo: vista SQL que devuelve el tipo de datos xml generado  
 La siguiente definición de vista SQL crea una vista XML de una columna relacional, pk, y de los autores de libros recuperados de una columna XML:  
  
```  
CREATE VIEW V (xmlVal) AS  
SELECT pk, xCol.query('/book/author')  
FROM   T  
FOR XML AUTO, TYPE  
```  
  
 La vista V contiene una sola fila con una sola columna xmlval de tipo XML `.` que se puede consultar como una `xml` instancia de tipo de datos normal. Por ejemplo, la siguiente consulta devuelve el autor cuyo nombre es "David":  
  
```  
SELECT xmlVal.query('//author[first-name = "David"]')  
FROM   V  
```  
  
 Las definiciones de vistas SQL son en cierto modo similares a las vistas XML que se crean mediante esquemas anotados. Sin embargo, hay tres diferencias importantes. La definición de vista SQL es de solo lectura y se debe manipular con XQuery incrustado. Las vistas XML se crean mediante un esquema anotado. Además, la vista SQL materializa el resultado XML antes de aplicar la expresión XQuery, mientras que las consultas XPath en las vistas XML evalúan consultas SQL en las tablas subyacentes.  
  
## <a name="see-also"></a>Consulte también  
 [FOR XML &#40;SQL Server&#41;](for-xml-sql-server.md)  
  
  
