---
title: Uso de sintaxis en una expresión de ruta de acceso se abrevia como | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- axis step [XQuery]
- abbreviated syntax [XQuery]
ms.assetid: f83c2e41-5722-47c3-b5b8-bf0f8cbe05d3
caps.latest.revision: 23
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 30a856638a4210c964f3e10311e99f4ddf69fd91
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33077602"
---
# <a name="path-expressions---using-abbreviated-syntax"></a>Expresiones de ruta de acceso: mediante sintaxis abreviada
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Todos los ejemplos de [descripción de las expresiones de ruta de acceso de XQuery](../xquery/path-expressions-xquery.md) utilizan sintaxis no abreviada para las expresiones de ruta de acceso. La sintaxis no abreviada para un paso de eje en una expresión de ruta de acceso incluye el nombre del eje y la prueba de nodo, separados por dos puntos dobles, y seguidos por cero o más calificadores de paso.  
  
 Por ejemplo:  
  
```  
child::ProductDescription[attribute::ProductModelID=19]  
```  
  
 XQuery admite las siguientes abreviaturas para usarlas con expresiones de ruta de acceso:  
  
-   El **secundarios** eje es el eje predeterminado. Por lo tanto, la **secundarios::** eje puede omitirse en un paso en una expresión. Por ejemplo, `/child::ProductDescription/child::Summary` puede escribirse como `/ProductDescription/Summary`.  
  
-   Un **atributo** eje se puede abreviar como @. Por ejemplo, `/child::ProductDescription[attribute::ProductModelID=10]` puede escribirse como `/ProudctDescription[@ProductModelID=10]`.  
  
-   A **/descendant-or-self::node()/** puede abreviarse como / /. Por ejemplo, `/descendant-or-self::node()/child::act:telephoneNumber` puede escribirse como `//act:telephoneNumber`.  
  
     La consulta anterior recupera todos los números de teléfono almacenados en la columna AdditionalContactInfo de la tabla Contact. El esquema para AdditionalContactInfo se define de forma que un \<telephoneNumber > elemento puede aparecer en cualquier lugar en el documento. Por tanto, para recuperar todos los números de teléfono, debe buscar cada nodo del documento. Esta búsqueda se inicia en la raíz del documento y continúa en todos los nodos descendientes.  
  
     La consulta siguiente recupera todos los números de teléfono para un contacto de cliente específico:  
  
    ```  
    SELECT AdditionalContactInfo.query('             
                declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";             
                declare namespace crm="http://schemas.adventure-works.com/Contact/Record";             
                declare namespace ci="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";             
                /descendant-or-self::node()/child::act:telephoneNumber             
                ') as result             
    FROM Person.Contact             
    WHERE ContactID=1             
    ```  
  
     Si reemplaza la expresión de ruta de acceso por la sintaxis abreviada, `//act:telephoneNumber`, obtendrá los mismos resultados.  
  
-   El **self::node()** en un paso puede abreviarse con un punto (.). Sin embargo, el punto no es equivalente o intercambiable con la **self::node()**.  
  
     Por ejemplo, en la consulta siguiente, el uso de un punto representa un valor y no un nodo:  
  
    ```  
    ("abc", "cde")[. > "b"]  
    ```  
  
-   El **parent::node()** en un paso puede abreviarse con un doble punto (.).  
  
  
