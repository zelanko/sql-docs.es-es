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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d3d7a76c67096d2e76fe1cd3d4b15f73122699e7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302806"
---
# <a name="interoperability-of-sql-statements"></a>Interoperabilidad de instrucciones SQL
Al igual que el resto de una aplicación, las instrucciones SQL pueden ser interoperables o específicas del DBMS. Y, al igual que el resto de la aplicación, la elección de cómo las instrucciones SQL interoperables deben depender del tipo de aplicación. Es menos probable que las aplicaciones personalizadas usen instrucciones SQL interoperables porque normalmente están diseñadas para aprovechar las capacidades de uno o posiblemente dos DBMS. Las aplicaciones genéricas usan instrucciones SQL interoperables porque están diseñadas para trabajar con diversos DBMS. Y las aplicaciones verticales normalmente se encuentran en algún lugar entre, lo que exige cierto nivel de funcionalidad pero, de lo contrario, usa instrucciones SQL interoperables.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Elegir una gramática SQL](../../../odbc/reference/develop-app/choosing-an-sql-grammar.md)  
  
-   [Crear instrucciones SQL Interoperable](../../../odbc/reference/develop-app/constructing-interoperable-sql-statements.md)
