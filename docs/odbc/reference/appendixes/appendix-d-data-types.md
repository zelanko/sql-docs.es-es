---
title: 'Apéndice D: tipos de datos | Documentos de Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- C data types [ODBC], defined
- SQL data types [ODBC], defined
- data types [ODBC]
- data types [ODBC], about data types
ms.assetid: 981d49c3-3531-4543-aa75-5bd9e4f67000
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 04d25dd57849514636c53092276ef49dc44187bf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="appendix-d-data-types"></a>Apéndice D: tipos de datos
ODBC define dos conjuntos de tipos de datos: SQL tipos de datos de C y tipos de datos. Tipos de datos SQL indican el tipo de datos de los datos almacenados en el origen de datos. Tipos de datos C indican el tipo de datos de los datos almacenados en los búferes de la aplicación.  
  
 Tipos de datos SQL se definen por cada DBMS según el estándar SQL-92. Para cada tipo de datos SQL especificado en el estándar SQL-92, ODBC define un identificador de tipo, que es un **#define** valor que se pasa como argumento en las funciones ODBC o se devuelva en los metadatos de un conjunto de resultados. El SQL-92 solo tipos de datos no admitidos por ODBC son bits (el tipo de ODBC SQL_BIT tiene características diferentes), BIT_VARYING, TIME_WITH_TIMEZONE, TIMESTAMP_WITH_TIMEZONE y NATIONAL_CHARACTER. Los controladores son responsables de asignar tipos de datos SQL específico del origen de datos a los identificadores de tipo de datos SQL de ODBC y los identificadores de tipo de datos SQL específico del controlador. El tipo de datos SQL se especifica en el campo SQL_DESC_CONCISE_TYPE de un descriptor de implementación.  
  
 ODBC define los tipos de datos de C y sus identificadores de tipo ODBC correspondientes. Una aplicación especifica el tipo de datos de C del búfer que recibirá los datos del conjunto de resultados al pasar el identificador de tipo C apropiado en el *TargetType* argumento en una llamada a **SQLBindCol** o  **SQLGetData**. Especifica el tipo C de búfer que contiene un parámetro de instrucción pasando el identificador de tipo C apropiado en el *ValueType* argumento en una llamada a **SQLBindParameter**. El tipo de datos de C se especifica en el campo SQL_DESC_CONCISE_TYPE de un descriptor de la aplicación.  
  
> [!NOTE]  
>  No hay ningún tipo de datos C específicos del controlador.  
  
 Cada tipo de datos SQL corresponde a un tipo de datos C de ODBC. Antes de devolver los datos del origen de datos, el controlador lo convierte en el tipo de datos C especificado. Antes de enviar datos al origen de datos, el controlador convierte del tipo de datos C especificado.  
  
 Este apéndice contiene los temas siguientes.  
  
-   [Usar identificadores de tipo de datos](../../../odbc/reference/appendixes/using-data-type-identifiers.md)  
  
-   [Tipos de datos SQL](../../../odbc/reference/appendixes/sql-data-types.md)  
  
-   [Tipos de datos C](../../../odbc/reference/appendixes/c-data-types.md)  
  
-   [Identificadores y descriptores de tipo de datos](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)  
  
-   [Identificadores de pseudotipo](../../../odbc/reference/appendixes/pseudo-type-identifiers.md)  
  
-   [Transferencia de datos en su forma binaria](../../../odbc/reference/appendixes/transferring-data-in-its-binary-form.md)  
  
-   [Directrices para los tipos de datos numéricos y de intervalo](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md)  
  
-   [Restricciones del calendario gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)  
  
-   [Tamaño de columna, dígitos decimales, longitud de transferencia y tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)  
  
-   [Convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)  
  
-   [Convertir datos de C en tipos de datos SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)  
  
 Para obtener una explicación de los tipos de datos ODBC, vea [tipos de datos de ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md). Para obtener información acerca de los tipos de datos SQL específico del controlador, consulte la documentación del controlador.
