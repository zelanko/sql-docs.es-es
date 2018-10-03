---
title: espacio de nombres-uri-from-QName (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:namespace-uri-from-QName function
- namespace-uri-from-QName function
ms.assetid: 4ab3f003-2a3b-4268-9e88-b615e35701b2
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ff8783eee040064e016becebc64e041e1dca4ce0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47808074"
---
# <a name="functions-related-to-qnames---namespace-uri-from-qname"></a>Funciones relacionadas con QNames: namespace-uri-from-QName
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve una cadena que representa el uri de espacio de nombres del QName especificado por *$arg*. El resultado es una secuencia vacía si *$arg* es una secuencia vacía.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
namespace-uri-from-QName($arg as xs:QName?) as xs:string?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Valor QName para el que se devuelve el URI del espacio de nombres.  
  
## <a name="examples"></a>Ejemplos  
 En este tema se proporciona ejemplos de XQuery con instancias XML almacenadas en varias **xml** columnas de tipo en la base de datos AdventureWorks.  
  
### <a name="a-retrieve-the-namespace-uri-from-a-qname"></a>A. Recuperar el URI del espacio de nombres de un valor QName  
 Para obtener un ejemplo funcional, consulte [nombre local de QName &#40;XQuery&#41;](../xquery/functions-related-to-qnames-local-name-from-qname.md).  
  
### <a name="implementation-limitations"></a>Limitaciones de la implementación  
 Éstas son las limitaciones:  
  
-   El **namespace-uri-from-QName()** función devuelve instancias de xs: String en lugar de xs: anyURI.  
  
## <a name="see-also"></a>Vea también  
 [Funciones relacionadas con QNames &#40;XQuery&#41;](http://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
