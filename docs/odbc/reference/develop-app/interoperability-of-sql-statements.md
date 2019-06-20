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
manager: craigg
ms.openlocfilehash: c4ead7cf96ada6d6055bc676ecf4610f2cf4c8f1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62446665"
---
# <a name="interoperability-of-sql-statements"></a>Interoperabilidad de instrucciones SQL
Igual que el resto de una aplicación, pueden ser instrucciones SQL interoperable o específicos para DBMS. Y como el resto de la aplicación, la elección de instrucciones SQL interoperables cómo deben ser depende del tipo de aplicación. Están menos probable que use instrucciones SQL interoperables porque normalmente están diseñadas para aprovechar las capacidades del DBMS de uno o dos, posiblemente, las aplicaciones personalizadas. Aplicaciones genéricas usar instrucciones SQL interoperables porque están diseñadas para funcionar con una variedad de DBMS. Y aplicaciones verticales suelen clasificarse en algún lugar entre ambos, exigir un cierto nivel de funcionalidad, pero en caso contrario, usar instrucciones SQL interoperables.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Elegir una gramática SQL](../../../odbc/reference/develop-app/choosing-an-sql-grammar.md)  
  
-   [Crear instrucciones SQL Interoperable](../../../odbc/reference/develop-app/constructing-interoperable-sql-statements.md)
