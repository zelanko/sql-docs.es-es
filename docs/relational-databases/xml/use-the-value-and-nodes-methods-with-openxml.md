---
title: Usar los métodos value() y nodes() con OPENXML | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- OpenXML method [XML in SQL Server]
- value method [XML in SQL Server]
- nodes method [XML in SQL Server]
ms.assetid: c73dbe55-d685-42eb-b0ee-9f3c5b9d97f3
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2764b3a51245a1c6248cd384e9bb3fec57d47d25
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="use-the-value-and-nodes-methods-with-openxml"></a>Utilizar los métodos de valor() y nodos() con OPENXML
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Puede usar varios métodos **value()** en el tipo de datos **xml** de una cláusula **SELECT** para generar un conjunto de filas de valores extraídos. El método **nodes()** da como resultado una referencia interna para cada nodo seleccionado, que se puede usar para hacer más consultas. La combinación de los métodos **nodes()** y **value()** puede ser más eficaz para generar el conjunto de filas cuando tiene varias columnas y, tal vez, cuando las expresiones de ruta de acceso empleadas en su generación son complejas.  
  
 El método **nodes()** da como resultado instancias de un tipo de datos **xml** especial, cada una de las cuales tiene su contexto establecido en un nodo seleccionado diferente. Este tipo de instancia XML admite los métodos **query()**, **value()**, **nodes()** y **exist()** y se puede usar en agregaciones **count(\*)**. Otros usos generarían un error.  
  
## <a name="example-using-nodes"></a>Ejemplo: utilizar nodes()  
 Suponga que desea extraer el nombre y los apellidos de los autores cuyo nombre no sea "David". Además, desea extraer esta información como un conjunto de filas que contiene dos columnas: FirstName y LastName. Con los métodos **nodes()** y **value()** puede lograrlo, como se indica aquí:  
  
```  
SELECT nref.value('(first-name/text())[1]', 'nvarchar(50)') FirstName,  
       nref.value('(last-name/text())[1]', 'nvarchar(50)') LastName  
FROM   T CROSS APPLY xCol.nodes('//author') AS R(nref)  
WHERE  nref.exist('first-name[. != "David"]') = 1  
```  
  
 En este ejemplo, `nodes('//author')` da como resultado un conjunto de filas de referencias a elementos `<author>` para cada instancia XML. Los nombres y apellidos de los autores se obtienen evaluando los métodos **value()** relativos a esas referencias.  
  
 SQL Server 2000 permite generar un conjunto de filas a partir de una instancia XML con **OpenXml()**. Puede especificar el esquema relacional para el conjunto de filas y la manera en que se asignan los valores dentro de la instancia XML a columnas del conjunto de filas.  
  
## <a name="example-using-openxml-on-the-xml-data-type"></a>Ejemplo: utilizar OpenXml() en el tipo de datos xml  
 La consulta se puede volver a escribir a partir del ejemplo anterior usando **OpenXml()** como se indica aquí. Para ello, se crea un cursor que lee cada instancia XML en una variable XML y luego le aplica OpenXML:  
  
```  
DECLARE name_cursor CURSOR  
FOR  
   SELECT xCol   
   FROM   T  
OPEN name_cursor  
DECLARE @xmlVal XML  
DECLARE @idoc int  
FETCH NEXT FROM name_cursor INTO @xmlVal  
  
WHILE (@@FETCH_STATUS = 0)  
BEGIN  
   EXEC sp_xml_preparedocument @idoc OUTPUT, @xmlVal  
   SELECT   *  
   FROM   OPENXML (@idoc, '//author')  
          WITH (FirstName  varchar(50) 'first-name',  
                LastName   varchar(50) 'last-name') R  
   WHERE  R.FirstName != 'David'  
  
   EXEC sp_xml_removedocument @idoc  
   FETCH NEXT FROM name_cursor INTO @xmlVal  
END  
CLOSE name_cursor  
DEALLOCATE name_cursor   
```  
  
 **OpenXml()** crea una representación en la memoria y usa tablas de trabajo en lugar del procesador de consultas. Se basa en el procesador de XPath versión 1.0 de MSXML versión 3.0 en lugar del motor de XQuery. Las tablas de trabajo no se comparten entre varias llamadas a **OpenXml()**, ni siquiera en la misma instancia XML. Esto limita su escalabilidad. **OpenXml()** permite el acceso a un formato de tabla irregular para los datos XML cuando no se especifica la cláusula WITH. Además, permite utilizar el valor XML restante en una columna de "desbordamiento" independiente.  
  
 En la combinación de las funciones **nodes()** y **value()** se usan índices XML con eficacia. Como resultado, esta combinación puede ofrecer una mayor escalabilidad que **OpenXml**.  
  
## <a name="see-also"></a>Ver también  
 [OPENXML &#40;SQL Server&#41;](../../relational-databases/xml/openxml-sql-server.md)  
  
  
