---
title: "Prólogo de XQuery | Documentos de Microsoft"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- XQuery, prolog
- prolog
- namespaces [XQuery]
- default namespace declarations
ms.assetid: 03924684-c5fd-44dc-8d73-c6ab90f5e069
caps.latest.revision: "26"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b007a65129ad217dea6ccb1f099211618c309851
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="modules-and-prologs---xquery-prolog"></a>Módulos y prólogos - prólogo de XQuery
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Una consulta XQuery se compone de un prólogo y un cuerpo. El prólogo de una consulta XQuery consiste en una serie de declaraciones y definiciones que, juntas, crean el entorno necesario para el procesamiento de la consulta. En SQL Server, el prólogo de una consulta XQuery puede incluir declaraciones de espacio de nombres. El cuerpo de una consulta XQuery está formado por una secuencia de expresiones que especifican el resultado previsto de la consulta.  
  
 Por ejemplo, la siguiente consulta XQuery se especifica en la columna Instructions de **xml** tipo que almacena las instrucciones de fabricación como XML. La consulta recupera las instrucciones de fabricación para la ubicación del centro de trabajo `10`. El `query()` método de la **xml** tipo de datos se utiliza para especificar la expresión XQuery.  
  
```  
SELECT Instructions.query('declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";           
    /AWMI:root/AWMI:Location[@LocationID=10]  
') AS Result   
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   El prólogo de XQuery incluye una declaración de prefijo (AWMI) de espacio de nombres, `(namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";`.  
  
-   La palabra clave `declare namespace` define un prefijo de espacio de nombres que se utiliza posteriormente en el cuerpo de la consulta.  
  
-   `/AWMI:root/AWMI:Location[@LocationID="10"]` es el cuerpo de la consulta.  
  
## <a name="namespace-declarations"></a>Declaraciones de espacios de nombres  
 Una declaración de espacio de nombres define un prefijo y lo asocia a un URI de espacio de nombres, como se muestra en la consulta siguiente. En la consulta, `CatalogDescription` es un **xml** columna de tipo.  
  
 Al especificar una consulta XQuery en esta columna, el prólogo de la consulta incluye la declaración `declare namespace` para asociar el prefijo `PD` (descripción del producto) al URI de espacio de nombres. Después, este prefijo se utiliza en el cuerpo de la consulta en lugar del URI de espacio de nombres. Los nodos del XML resultante están en el espacio de nombres asociado al URI de espacio de nombres.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
         /PD:ProductDescription/PD:Summary   
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 Para mejorar la legibilidad de la consulta, los espacios de nombres se pueden declarar con WITH XMLNAMESPACES en lugar de declarar enlaces de prefijos y espacios de nombres con `declare namespace` en el prólogo.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD)  
  
SELECT CatalogDescription.query('  
         /PD:ProductDescription/PD:Summary   
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 Para obtener más información, vea, [agregar espacios de nombres a consultas con WITH XMLNAMESPACES](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md).  
  
### <a name="default-namespace-declaration"></a>Declaración del espacio de nombres predeterminado  
 En lugar de declarar un prefijo de espacio de nombres mediante la declaración `declare namespace`, se puede utilizar la declaración `declare default element namespace` para enlazar un espacio de nombres predeterminado para nombres de elementos. En este caso, no se especifica ningún prefijo.  
  
 En el ejemplo siguiente, la expresión de ruta de acceso del cuerpo de la consulta no especifica ningún prefijo de espacio de nombres. De manera predeterminada, todos los nombres de elementos pertenecen al espacio de nombres predeterminado especificado en el prólogo.  
  
```  
SELECT CatalogDescription.query('  
     declare default element namespace  "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
        /ProductDescription/Summary   
    ') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID=19   
```  
  
 Para declarar un espacio de nombres predeterminado, se puede utilizar WITH XMLNAMESPACES:  
  
```  
WITH XMLNAMESPACES (DEFAULT 'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription')  
SELECT CatalogDescription.query('  
        /ProductDescription/Summary   
    ') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID=19   
```  
  
## <a name="see-also"></a>Vea también  
 [Agregar espacios de nombres a consultas con WITH XMLNAMESPACES](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)  
  
  
