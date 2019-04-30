---
title: Cumplimiento de la interfaz de nivel 1 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- level 1 interface conformance levels [ODBC]
ms.assetid: ee3f5c08-0583-4f3b-8354-ef71b6086a7e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8d75c374a7d9d57483dd56e34b51fcb6d89e1b52
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63213486"
---
# <a name="level-1-interface-conformance"></a>Cumplimiento de la interfaz de nivel 1
El nivel de conformidad de interfaz de nivel 1 incluye la funcionalidad de nivel de conformidad de interfaz de Core además de características adicionales, como las transacciones, que suelen estar disponibles en un DBMS relacional OLTP. Un controlador de función de la interfaz de nivel 1 permite que la aplicación haga lo siguiente, además de las características en el nivel de conformidad de interfaz de núcleo:  
  
|||  
|-|-|  
|101|Especifique el esquema de base de datos de las tablas y vistas (con nombres de dos partes). (Para obtener más información, vea la nomenclatura de tres partes característica 201 en [cumplimiento de la interfaz de nivel 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)|  
|102|Invocar true ejecución asincrónica de las funciones ODBC, donde las funciones ODBC aplicables son todas sincrónicas o todas asincrónicas en una conexión determinada.|  
|103|Usar cursores desplazables y, por tanto, obtener acceso a un conjunto de resultados en los métodos que no sea de solo avance, mediante una llamada a **SQLFetchScroll** con el *FetchOrientation* argumento distinto de SQL_FETCH_NEXT. (El SQL_FETCH_BOOKMARK *FetchOrientation* está en la característica 204 en [cumplimiento de la interfaz de nivel 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)|  
|104|Obtener las claves principales de tablas, mediante una llamada a **SQLPrimaryKeys**.|  
|105|Utilice los procedimientos almacenados, a través de la secuencia de escape ODBC para las llamadas de procedimiento y consultar el diccionario de datos con respecto a los procedimientos almacenados, mediante una llamada a **SQLProcedureColumns** y **SQLProcedures**. (El proceso por el que los procedimientos se crean y almacenan en el origen de datos está fuera del ámbito de este documento).|  
|106|Conectarse a un origen de datos a través de forma interactiva los servidores disponibles, mediante una llamada a **SQLBrowseConnect**.|  
|107|Utilice las funciones ODBC en lugar de instrucciones SQL para realizar determinadas operaciones de base de datos: **SQLSetPos** con SQL_POSITION y SQL_REFRESH.|  
|108|Obtener acceso al contenido de varios conjuntos de resultados generados por lotes y procedimientos almacenados, mediante una llamada a **SQLMoreResults**.|  
|109|Delimitar las transacciones que abarcan varias funciones ODBC, con atomicidad y la capacidad de especificar SQL_ROLLBACK en **SQLEndTran**.|
