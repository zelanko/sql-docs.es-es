---
title: Interoperabilidad de instrucciones SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC]
- interoperability of SQL statements [ODBC], about interoperability
ms.assetid: 3b24c499-829c-4e65-90cf-a3a0f6d0a186
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ed366acde11778342387d3bcb152a6619a6a3778
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138865"
---
# <a name="interoperability-of-sql-statements"></a>Interoperabilidad de instrucciones SQL
Igual que el resto de una aplicación, pueden ser instrucciones SQL interoperable o específicos para DBMS. Y como el resto de la aplicación, la elección de instrucciones SQL interoperables cómo deben ser depende del tipo de aplicación. Están menos probable que use instrucciones SQL interoperables porque normalmente están diseñadas para aprovechar las capacidades del DBMS de uno o dos, posiblemente, las aplicaciones personalizadas. Aplicaciones genéricas usar instrucciones SQL interoperables porque están diseñadas para funcionar con una variedad de DBMS. Y aplicaciones verticales suelen clasificarse en algún lugar entre ambos, exigir un cierto nivel de funcionalidad, pero en caso contrario, usar instrucciones SQL interoperables.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Elegir una gramática SQL](../../../odbc/reference/develop-app/choosing-an-sql-grammar.md)  
  
-   [Crear instrucciones SQL Interoperable](../../../odbc/reference/develop-app/constructing-interoperable-sql-statements.md)
