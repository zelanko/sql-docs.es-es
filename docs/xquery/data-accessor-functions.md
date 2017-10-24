---
title: Funciones de descriptor de acceso de datos | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- data-accessor functions [XQuery]
ms.assetid: 31bad04f-7c74-4773-9f83-612704fdd21c
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 456d359fd407e305bc8bfb3b85bd29b7bada8382
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="data-accessor-functions"></a>Funciones del descriptor de acceso a datos
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  En los temas expuestos en esta sección se ofrecen descripciones y ejemplos de código para las funciones del descriptor de acceso a datos.  
  
## <a name="understanding-fndata-fnstring-and-text"></a>Información acerca de fn:data (), fn:string () y text()  
 XQuery tiene una función **fn:Data()** para extraer valores escalares con tipo de nodos, una prueba de nodo **text()** para devolver los nodos de texto y la función **fn:String()** que devuelve el valor de cadena de un nodo. Su uso puede resultar confuso. A continuación, se presentan las directrices para usarlas correctamente en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. La instancia XML \<age > 12 \< /age > se utiliza con fines ilustrativos.  
  
-   XML sin tipo: la expresión de ruta de acceso /age/text() devuelve el nodo de texto "12". La función fn:data(/age) devuelve el valor de cadena "12", igual que fn:string(/age).  
  
-   XML con tipo: La expresión /age/text() devuelve un error estático para cualquier tipada simple \<age > elemento. Por otro lado, fn:data (/edad) devuelve el entero 12. La función fn:string(/age) produce la cadena "12".  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [cadena Function &#40; XQuery &#41;](../xquery/data-accessor-functions-string-xquery.md)  
  
-   [Función de datos &#40; XQuery &#41;](../xquery/data-accessor-functions-data-xquery.md)  
  
## <a name="see-also"></a>Vea también  
 [Expresiones de ruta de acceso &#40; XQuery &#41;](../xquery/path-expressions-xquery.md)  
  
  

