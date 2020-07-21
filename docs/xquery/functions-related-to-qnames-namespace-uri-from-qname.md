---
title: namespace-uri-from-QName (XQuery) | Microsoft Docs
description: Obtenga información sobre cómo usar la función namespace-uri-from-QName para recuperar el URI de espacio de nombres de un QName.
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:namespace-uri-from-QName function
- namespace-uri-from-QName function
ms.assetid: 4ab3f003-2a3b-4268-9e88-b615e35701b2
author: rothja
ms.author: jroth
ms.openlocfilehash: 91174fa3ef113a7944ef02bb62e7088acd344f3e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85720040"
---
# <a name="functions-related-to-qnames---namespace-uri-from-qname"></a>Funciones relacionadas con QNames: namespace-uri-from-QName
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  Devuelve una cadena que representa el URI de espacio de nombres del QName especificado por *$arg*. El resultado es una secuencia vacía si *$arg* es la secuencia vacía.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
namespace-uri-from-QName($arg as xs:QName?) as xs:string?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Valor QName para el que se devuelve el URI del espacio de nombres.  
  
## <a name="examples"></a>Ejemplos  
 En este tema se proporcionan ejemplos de XQuery con instancias XML almacenadas en varias columnas de tipo **XML** de la base de datos AdventureWorks.  
  
### <a name="a-retrieve-the-namespace-uri-from-a-qname"></a>A. Recuperar el URI del espacio de nombres de un valor QName  
 Para obtener un ejemplo funcional, vea [nombre-de-local-de-QName &#40;XQuery&#41;](../xquery/functions-related-to-qnames-local-name-from-qname.md).  
  
### <a name="implementation-limitations"></a>Limitaciones de la implementación  
 Éstas son las limitaciones:  
  
-   La función **namespace-uri-from-QName ()** devuelve instancias de XS: String en lugar de XS: anyURI.  
  
## <a name="see-also"></a>Consulte también  
 [Funciones relacionadas con QNames &#40;XQuery&#41;](https://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
