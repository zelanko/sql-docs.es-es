---
description: Características para vigilar
title: Características que se deben inspeccionar | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], writing interoperable applications
ms.assetid: 0fb1693b-11c3-43b1-bb16-c3323b7b2d45
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ee7da25bccf0ed3d3649412c702a426a31c3ad44
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499905"
---
# <a name="features-to-watch-for"></a>Características para vigilar
En esta sección se describen varias características que los desarrolladores de aplicaciones suelen tomar para concedidos. De hecho, estas características varían considerablemente en cuanto a compatibilidad y modo de compatibilidad entre DBMS; Si no se produce código para ellos, es probable que se produzcan problemas en aplicaciones interoperables.  
  
 En esta sección no se muestran todas las características que los desarrolladores de aplicaciones deben tener en cuenta. Para obtener esa información, consulte las descripciones de las funciones [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md), [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)y [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) , [Apéndice C: gramática de SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)y las secciones de este manual que describen cada característica.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Número de versión](../../../odbc/reference/develop-app/version-number.md)  
  
-   [Varias instrucciones activas y las conexiones](../../../odbc/reference/develop-app/multiple-active-statements-and-connections.md)  
  
-   [Compatibilidad con transacciones en DBMS](../../../odbc/reference/develop-app/transaction-support-in-dbmss.md)  
  
-   [Confirmación y el comportamiento de reversión](../../../odbc/reference/develop-app/commit-and-rollback-behavior.md)  
  
-   [NOT NULL en las instrucciones de CREATE TABLE](../../../odbc/reference/develop-app/not-null-in-create-table-statements.md)  
  
-   [Tipos de datos admitidos](../../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md)  
  
-   [Gramática de SQL de ODBC](../../../odbc/reference/develop-app/odbc-sql-grammar.md)  
  
-   [Procesamiento por lotes](../../../odbc/reference/develop-app/batch-processing.md)
