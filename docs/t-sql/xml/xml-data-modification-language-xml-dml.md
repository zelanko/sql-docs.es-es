---
title: "Lenguaje de manipulación de datos XML (XML DML) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- modifying data [SQL Server], XML DML
- XML [SQL Server], DML
- XML DML [SQL Server]
- data modification language [XML DML]
- data modifications [XML DML]
- DML [XML in SQL Server]
- XQuery, XML DML
- xml data type [SQL Server], XML DML
ms.assetid: 20ce50d2-c07b-4e41-93a7-1380d2cd49cb
caps.latest.revision: "29"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5b3315bad83aff77c661edb9e0b3e9e081147d42
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/19/2018
---
# <a name="xml-data-modification-language-xml-dml"></a>Lenguaje de manipulación de datos XML (XML DML)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El Lenguaje de manipulación de datos XML (XML DML) es una extensión del lenguaje XQuery. Según W3C, el lenguaje XQuery carece de la parte de manipulación de datos (DML). El DML de XML que se presenta en este tema así como el lenguaje de XQuery, proporciona una consulta totalmente funcional y el lenguaje de manipulación de datos que se puede usar con la **xml** tipo de datos.  
  
 XML DML agrega a XQuery las siguientes palabras clave, donde se distingue entre mayúsculas y minúsculas:  
  
-   **insert**  
  
-   **delete**  
  
-   **Reemplace el valor de**  
  
 Como se describe en [tipo de datos XML y columnas &#40; SQL Server &#41; ](../../relational-databases/xml/xml-data-type-and-columns-sql-server.md), puede crear variables y columnas de la **xml** escriba y asignarles documentos o fragmentos XML. Para modificar o actualizar estas instancias XML, realice el siguiente procedimiento:  
  
-   Utilice la [tipo de datos de xml de método modify())](../../t-sql/xml/modify-method-xml-data-type.md) de la **xml** tipo de datos.  
  
-   Especificar las instrucciones XML DML correspondientes dentro de la **modify()** método.  
  
 Tenga en cuenta que no se pueden insertar ni eliminar algunos atributos, y a veces tampoco es posible modificar sus valores. Por ejemplo:  
  
-   Para con o sin tipo **xml,** los atributos son **xmlns**, **xmlns:\***, y **XML: base**.  
  
-   Para tipos de **xml** únicamente, los atributos son **xsi: nil**, y **xsi: Type**.  
  
 Entre otras restricciones se pueden citar las siguientes:  
  
-   Para con o sin tipo **xml**, insertar el atributo **XML: base** se producirá un error.  
  
-   Para tipos de **xml**, eliminar y modificar el **xsi: nil** se producirá un error de atributo. Sin tipo **xml**, puede eliminar el atributo o modificar su valor.  
  
-   Para tipos de **xml**, modificar el valor de la **xs: Type** se producirá un error de atributo. Sin tipo **xml**, puede modificar el valor del atributo.  
  
 Cuando se modifica una instancia XML con tipo, el formato final debe ser una instancia válida de ese tipo. En caso contrario, se devuelve un error de validación.  
  
## <a name="see-also"></a>Vea también  
 [Insert &#40; XML DML &#41;](../../t-sql/xml/insert-xml-dml.md)   
 [Eliminar &#40; XML DML &#41;](../../t-sql/xml/delete-xml-dml.md)   
 [valor de reemplazo de &#40; XML DML &#41;](../../t-sql/xml/replace-value-of-xml-dml.md)   
 [Comparar XML con tipo y XML sin tipo](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Crear instancias de datos XML](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [Métodos del tipo de datos xml](../../t-sql/xml/xml-data-type-methods.md)  
  
  
