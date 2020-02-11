---
title: Conformidad con la interfaz de nivel 1 | Microsoft Docs
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
ms.openlocfilehash: 05cf381ccbb8c0747db88259acfb4ba218d3e0ae
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68135012"
---
# <a name="level-1-interface-conformance"></a>Cumplimiento de la interfaz de nivel 1
El nivel de conformidad de la interfaz de nivel 1 incluye la funcionalidad del nivel de conformidad de la interfaz básica más características adicionales, como transacciones, que suelen estar disponibles en un DBMS relacional de OLTP. Un controlador compatible con la interfaz de nivel 1 permite que la aplicación realice lo siguiente, además de las características del nivel de conformidad de la interfaz principal:  
  
|||  
|-|-|  
|101|Especifique el esquema de las tablas y vistas de base de datos (con nombres de dos partes). (Para obtener más información, vea la característica de nomenclatura de tres partes 201 en el cumplimiento de la [interfaz de nivel 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md)).|  
|102|Invocar la ejecución asincrónica verdadera de funciones ODBC, donde las funciones ODBC aplicables son todas sincrónicas o asincrónicas en una conexión determinada.|  
|103|Utilice cursores desplazables y, por tanto, conseguirá el acceso a un conjunto de resultados en métodos que no sean de solo avance, llamando a **SQLFetchScroll** con el argumento *FetchOrientation* que no sea SQL_FETCH_NEXT. (El SQL_FETCH_BOOKMARK *FetchOrientation* está en la característica 204 en el cumplimiento de la [interfaz de nivel 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md)).|  
|104|Obtener las claves principales de las tablas mediante una llamada a **SQLPrimaryKeys**.|  
|105|Use procedimientos almacenados, a través de la secuencia de escape ODBC para llamadas a procedimientos, y consulte el Diccionario de datos con respecto a los procedimientos almacenados llamando a **SQLProcedureColumns** y **SQLProcedures**. (El proceso por el que se crean y almacenan los procedimientos en el origen de datos está fuera del ámbito de este documento).|  
|106|Conéctese a un origen de datos mediante la exploración interactiva de los servidores disponibles mediante una llamada a **SQLBrowseConnect**.|  
|107|Usar funciones de ODBC en lugar de instrucciones SQL para realizar determinadas operaciones de base de datos: **SQLSetPos** con SQL_POSITION y SQL_REFRESH.|  
|108|Obtener acceso al contenido de varios conjuntos de resultados generados por lotes y procedimientos almacenados mediante una llamada a **SQLMoreResults**.|  
|109|Delimite las transacciones que abarcan varias funciones ODBC, con verdadera atomicidad y la capacidad de especificar SQL_ROLLBACK en **SQLEndTran**.|
