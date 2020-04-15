---
title: Conformidad de la interfaz de nivel 1 ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d31d5fe8aea1df4e7937104580efb820ba6f031
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306186"
---
# <a name="level-1-interface-conformance"></a>Cumplimiento de la interfaz de nivel 1
El nivel de conformidad de la interfaz de nivel 1 incluye la funcionalidad de nivel de conformidad de la interfaz principal, además de características adicionales, como transacciones, que normalmente están disponibles en un DBMS relacional OLTP. Un controlador compatible con la interfaz de nivel 1 permite a la aplicación hacer lo siguiente, además de las características del nivel de conformidad de la interfaz Core:  
  
|||  
|-|-|  
|101|Especifique el esquema de las tablas y vistas de base de datos (mediante la nomenclatura de dos partes). (Para obtener más información, consulte la característica de nomenclatura de tres partes 201 en Conformidad de [interfaz](../../../odbc/reference/develop-app/level-2-interface-conformance.md)de nivel 2 .)|  
|102|Invoque la ejecución asincrónica verdadera de funciones ODBC, donde las funciones ODBC aplicables son todas sincrónicas o asincrónicas en una conexión determinada.|  
|103|Utilice cursores desplazables y, por lo continuación, obtenga acceso a un conjunto de resultados en métodos distintos de solo avance, llamando a **SQLFetchScroll** con el *FetchOrientation* argumento distinto de SQL_FETCH_NEXT. (El SQL_FETCH_BOOKMARK *FetchOrientation* está en la característica 204 en conformidad de [interfaz](../../../odbc/reference/develop-app/level-2-interface-conformance.md)de nivel 2 .)|  
|104|Obtenga las claves principales de las tablas, llamando a **SQLPrimaryKeys**.|  
|105|Use procedimientos almacenados, a través de la secuencia de escape ODBC para las llamadas a procedimientos, y consulte el diccionario de datos con respecto a los procedimientos almacenados, llamando a **SQLProcedureColumns** y **SQLProcedures**. (El proceso por el cual se crean y almacenan los procedimientos en el origen de datos está fuera del ámbito de este documento.)|  
|106|Conéctese a un origen de datos examinando interactivamente los servidores disponibles, llamando a **SQLBrowseConnect**.|  
|107|Utilice funciones ODBC en lugar de instrucciones SQL para realizar determinadas operaciones de base de datos: **SQLSetPos** con SQL_POSITION y SQL_REFRESH.|  
|108|Obtenga acceso al contenido de varios conjuntos de resultados generados por lotes y procedimientos almacenados, llamando a **SQLMoreResults**.|  
|109|Delimite las transacciones que abarcan varias funciones ODBC, con verdadera atomicidad y la capacidad de especificar SQL_ROLLBACK en **SQLEndTran**.|
