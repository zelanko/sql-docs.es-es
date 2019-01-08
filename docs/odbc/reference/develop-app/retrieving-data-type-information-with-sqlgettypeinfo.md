---
title: Recuperación de datos de tipo de información con SQLGetTypeInfo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC], identifiers
- SQLGetTypeInfo function [ODBC], retrieving data type information
- retrieving data type information [ODBC]
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: d4f8b152-ab9e-4d05-a720-d10a08a6df81
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c69113e4bb5457cb997f832179e5c1aab2841d82
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52518869"
---
# <a name="retrieving-data-type-information-with-sqlgettypeinfo"></a>Al recuperar la información de tipo de datos con SQLGetTypeInfo
Dado que las asignaciones de tipos de datos SQL subyacentes a los identificadores de tipo ODBC son aproximadas, ODBC proporciona una función (**SQLGetTypeInfo**) a través de que un controlador completamente puede describir cada tipo de datos SQL en el origen de datos. Esta función devuelve un conjunto de resultados, cada fila de los cuales describe las características de un tipo de datos único, como nombre, identificador de tipo, precisión, escala y la nulabilidad.  
  
 Por lo general, esta información se usa por aplicaciones genéricas que permiten al usuario crear y modificar las tablas. Este tipo de aplicaciones llamada **SQLGetTypeInfo** para recuperar la información de tipo de datos y, a continuación, se presentan algunos o todos sus al usuario. Estas aplicaciones deben tener en cuenta dos cosas:  
  
-   Puede asignar más de un tipo de datos SQL a un identificador de tipo único, lo que puede dificultar a determinar qué tipo de datos para usar. Para resolver este problema, el conjunto de resultados se ordena por identificador de tipo y en segundo lugar está llegando a la definición del identificador de tipo. Además, los tipos de datos definido por el origen de datos tienen prioridad sobre los tipos de datos definido por el usuario. Por ejemplo, suponga que un origen de datos define los tipos de datos entero y el contador para que sean iguales, salvo que el contador es incremento automático. Supongamos también que el tipo definido por el usuario WHOLENUM es un sinónimo de entero. Cada uno de estos tipos se asigna a SQL_INTEGER. En el **SQLGetTypeInfo** conjunto de resultados, aparecerá entero en primer lugar, seguida de WHOLENUM y, a continuación, del contador. WHOLENUM aparece después de entero dado que es definido por el usuario, pero antes de contador porque más se aproxime la definición de la SQL_INTEGER el tipo de identificador.  
  
-   ODBC no define los nombres de tipo de datos para su uso en **CREATE TABLE** y **ALTER TABLE** instrucciones. En su lugar, debe usar el nombre devuelto en la columna TYPE_NAME del conjunto de resultados devuelto por la aplicación **SQLGetTypeInfo**. El motivo es que, aunque la mayoría de SQL no varían en gran parte a través de los DBMS, nombres de tipo de datos varían enormemente. En lugar de obligarle a controladores para analizar las instrucciones SQL y reemplace los nombres de tipo de datos estándar con nombres de tipo de datos específicos para DBMS, ODBC requiere que las aplicaciones para los nombres específicos para DBMS en primer lugar.  
  
 Tenga en cuenta que **SQLGetTypeInfo** describen necesariamente todos los tipos de datos que se puede encontrar una aplicación. En concreto, los conjuntos de resultados podrían contener tipos de datos no admitidos directamente el origen de datos. Por ejemplo, se definen los tipos de datos de las columnas de conjuntos de resultados devueltos por las funciones de catálogo ODBC y estos tipos de datos podrían no admitirse el origen de datos. Para determinar las características de los tipos de datos en un conjunto de resultados, una aplicación llama a **SQLColAttribute**.
