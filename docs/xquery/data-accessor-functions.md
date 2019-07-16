---
title: Funciones de descriptor de acceso de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- data-accessor functions [XQuery]
ms.assetid: 31bad04f-7c74-4773-9f83-612704fdd21c
author: rothja
ms.author: jroth
ms.openlocfilehash: b3726686a2c0e5229a0fccf4d9f51c0e1404f1a3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038953"
---
# <a name="data-accessor-functions"></a>Funciones del descriptor de acceso a datos
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  En los temas expuestos en esta sección se ofrecen descripciones y ejemplos de código para las funciones del descriptor de acceso a datos.  
  
## <a name="understanding-fndata-fnstring-and-text"></a>Información acerca de fn:data (), fn:string () y text()  
 XQuery tiene una función **fn:Data()** para extraer valores escalares con tipo de nodos, una prueba de nodo **text()** para devolver los nodos de texto y la función **fn:String()** que devuelve el valor de cadena de un nodo. Su uso puede resultar confuso. A continuación, se presentan las directrices para usarlas correctamente en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. La instancia XML \<age > 12 \< /age > se usa con fines ilustrativos.  
  
-   XML sin tipo: El /age/text() de expresión de ruta de acceso, se devuelve el nodo de texto "12". La función fn:data(/age) devuelve el valor de cadena "12", igual que fn:string(/age).  
  
-   XML con tipo: /Age/text() de la expresión devuelve un error para cualquier tipada simple estático \<age > elemento. Por otro lado, fn:data (/edad) devuelve el entero 12. La función fn:string(/age) produce la cadena "12".  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Función String &#40;XQuery&#41;](../xquery/data-accessor-functions-string-xquery.md)  
  
-   [Función datos &#40;XQuery&#41;](../xquery/data-accessor-functions-data-xquery.md)  
  
## <a name="see-also"></a>Vea también  
 [Expresiones de ruta &#40;XQuery&#41;](../xquery/path-expressions-xquery.md)  
  
  
