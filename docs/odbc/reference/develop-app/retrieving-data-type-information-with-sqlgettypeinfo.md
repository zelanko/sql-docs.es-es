---
title: "Recuperación de datos escriba información a SQLGetTypeInfo | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL data types [ODBC], identifiers
- SQLGetTypeInfo function [ODBC], retrieving data type information
- retrieving data type information [ODBC]
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: d4f8b152-ab9e-4d05-a720-d10a08a6df81
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8a1eb337e91595b5be013067847f73c3de117e97
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="retrieving-data-type-information-with-sqlgettypeinfo"></a>Al recuperar la información de tipo de datos con SQLGetTypeInfo
Dado que las asignaciones de tipos de datos SQL subyacentes a los identificadores de tipo ODBC son aproximadas, ODBC proporciona una función (**SQLGetTypeInfo**) a través de que un controlador completamente puede describir cada tipo de datos SQL en el origen de datos. Esta función devuelve un conjunto de resultados, cada fila de los cuales describe las características de un tipo de datos único, como nombre, identificador de tipo, precisión, escala y nulabilidad.  
  
 Por lo general, esta información se usa por aplicaciones genéricas que permiten al usuario crear y modificar las tablas. Tal aplicaciones llaman a **SQLGetTypeInfo** para recuperar la información de tipo de datos y, a continuación, presenta algunos o todos del mismo al usuario. Estas aplicaciones necesitan tener en cuenta dos cosas:  
  
-   Puede asignar más de un tipo de datos SQL a un identificador de tipo único, puede que le resulte difícil determinar qué tipo de datos para usar. Para resolver este problema, el conjunto de resultados se ordena por identificador de tipo y en segundo lugar por proximidad a la definición del identificador de tipo. Además, los tipos de datos definidos por el origen de datos tienen prioridad sobre los tipos de datos definidos por el usuario. Por ejemplo, suponga que un origen de datos define los tipos de datos entero y el contador para que sea el mismo, salvo que el contador es incremento automático. Supongamos también que el tipo definido por el usuario WHOLENUM es un sinónimo de entero. Cada uno de estos tipos se asigna a SQL_INTEGER. En el **SQLGetTypeInfo** conjunto de resultados, INTEGER aparece en primer lugar, seguido de WHOLENUM y, a continuación, del contador. WHOLENUM aparece después entero dado que es definido por el usuario, pero antes de contador porque más se ajuste a la definición de la SQL_INTEGER tipo identificador.  
  
-   ODBC no define los nombres de tipo de datos para su uso en **CREATE TABLE** y **ALTER TABLE** instrucciones. En su lugar, la aplicación debe utilizar el nombre devuelto en la columna TYPE_NAME del conjunto de resultados devuelto por **SQLGetTypeInfo**. La razón de ello es que, aunque la mayoría de SQL no varían en gran parte a través de DBMS, nombres de tipo de datos varían enormemente. En lugar de obligarle controladores para analizar las instrucciones SQL y reemplazar nombres de tipo de datos estándar con nombres de tipo de datos específicos de DBMS, ODBC requiere que las aplicaciones para usar los nombres específicos de DBMS en primer lugar.  
  
 Tenga en cuenta que **SQLGetTypeInfo** no necesariamente se describen todos los tipos de datos que se puede encontrar una aplicación. En concreto, los conjuntos de resultados podrían contener tipos de datos no es directamente compatibles con el origen de datos. Por ejemplo, se definen los tipos de datos de las columnas de conjuntos de resultados devueltos por funciones de catálogo de ODBC y pueden que el origen de datos no admite estos tipos de datos. Para determinar las características de los tipos de datos en un conjunto de resultados, una aplicación llama **SQLColAttribute**.

