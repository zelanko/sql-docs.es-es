---
title: Interoperabilidad de las instrucciones SQL ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d3d7a76c67096d2e76fe1cd3d4b15f73122699e7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302806"
---
# <a name="interoperability-of-sql-statements"></a>Interoperabilidad de instrucciones SQL
Al igual que el resto de una aplicación, las instrucciones SQL pueden ser interoperables o específicas de DBMS. Y al igual que el resto de la aplicación, la elección de cómo deben ser las instrucciones SQL interoperables depende del tipo de aplicación. Las aplicaciones personalizadas son menos propensas a utilizar instrucciones SQL interoperables porque normalmente están diseñadas para aprovechar las capacidades de uno o posiblemente dos DBMS. Las aplicaciones genéricas utilizan instrucciones SQL interoperables porque están diseñadas para trabajar con una variedad de DBMS. Y las aplicaciones verticales suelen caer en algún lugar intermedio, exigiendo un cierto nivel de funcionalidad, pero de lo contrario utilizando instrucciones SQL interoperables.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Elegir una gramática SQL](../../../odbc/reference/develop-app/choosing-an-sql-grammar.md)  
  
-   [Crear instrucciones SQL Interoperable](../../../odbc/reference/develop-app/constructing-interoperable-sql-statements.md)
