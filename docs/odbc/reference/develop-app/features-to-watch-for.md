---
title: Características para vigilar | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], writing interoperable applications
ms.assetid: 0fb1693b-11c3-43b1-bb16-c3323b7b2d45
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 704fc0c45706e80408218d185146a438099da829
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="features-to-watch-for"></a>Características para vigilar
Esta sección describe una serie de características que los desarrolladores de aplicaciones a menudo dan por sentado. De hecho, estas características varían ampliamente en soporte técnico y el modo de compatibilidad entre DBMS; errores al código para ellos es podría causar problemas en aplicaciones interoperables.  
  
 En esta sección no muestra todas las características que los desarrolladores de aplicaciones deben tener en cuenta. Para obtener esa información, consulte el [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md), [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md), y [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) función descripciones, [Apéndice C: SQL gramática](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)y las secciones de este manual que explican cada característica.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Número de versión](../../../odbc/reference/develop-app/version-number.md)  
  
-   [Varias instrucciones activas y las conexiones](../../../odbc/reference/develop-app/multiple-active-statements-and-connections.md)  
  
-   [Compatibilidad con transacciones en DBMS](../../../odbc/reference/develop-app/transaction-support-in-dbmss.md)  
  
-   [Confirmación y el comportamiento de reversión](../../../odbc/reference/develop-app/commit-and-rollback-behavior.md)  
  
-   [NOT NULL en las instrucciones de CREATE TABLE](../../../odbc/reference/develop-app/not-null-in-create-table-statements.md)  
  
-   [Tipos de datos admitidos](../../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md)  
  
-   [Gramática de SQL de ODBC](../../../odbc/reference/develop-app/odbc-sql-grammar.md)  
  
-   [Procesamiento por lotes](../../../odbc/reference/develop-app/batch-processing.md)
