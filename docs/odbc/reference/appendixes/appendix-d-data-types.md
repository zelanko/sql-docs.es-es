---
title: 'Apéndice D: Tipos de datos ? Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- C data types [ODBC], defined
- SQL data types [ODBC], defined
- data types [ODBC]
- data types [ODBC], about data types
ms.assetid: 981d49c3-3531-4543-aa75-5bd9e4f67000
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c1abadb962e3a1ee9327bbb8d84e52d180b4a7e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292465"
---
# <a name="appendix-d-data-types"></a>Apéndice D: Tipo de datos
ODBC define dos conjuntos de tipos de datos: tipos de datos SQL y tipos de datos C. Los tipos de datos SQL indican el tipo de datos almacenados en el origen de datos. Los tipos de datos C indican el tipo de datos almacenados en los búferes de aplicación.  
  
 Los tipos de datos SQL los define cada DBMS de acuerdo con el estándar SQL-92. Para cada tipo de datos SQL especificado en el estándar SQL-92, ODBC define un identificador de tipo, que es un valor **de #define** que se pasa como argumento en funciones ODBC o se devuelve en los metadatos de un conjunto de resultados. Los únicos tipos de datos SQL-92 no admitidos por ODBC son BIT (el tipo de SQL_BIT ODBC tiene características diferentes), BIT_VARYING, TIME_WITH_TIMEZONE, TIMESTAMP_WITH_TIMEZONE y NATIONAL_CHARACTER. Los controladores son responsables de asignar tipos de datos SQL específicos del origen de datos a identificadores de tipo de datos SQL ODBC e identificadores de tipo de datos SQL específicos del controlador. El tipo de datos SQL se especifica en el campo SQL_DESC_CONCISE_TYPE de un descriptor de implementación.  
  
 ODBC define los tipos de datos de C y sus identificadores de tipo ODBC correspondientes. Una aplicación especifica el tipo de datos C del búfer que recibirá datos del conjunto de resultados pasando el identificador de tipo C adecuado en el *argumento TargetType* en una llamada a **SQLBindCol** o **SQLGetData**. Especifica el tipo C del búfer que contiene un parámetro de instrucción pasando el identificador de tipo C adecuado en el argumento *ValueType* en una llamada a **SQLBindParameter**. El tipo de datos C se especifica en el campo SQL_DESC_CONCISE_TYPE de un descriptor de aplicación.  
  
> [!NOTE]  
>  No hay tipos de datos C específicos del controlador.  
  
 Cada tipo de datos SQL corresponde a un tipo de datos ODBC C. Antes de devolver datos del origen de datos, el controlador los convierte al tipo de datos C especificado. Antes de enviar datos al origen de datos, el controlador los convierte del tipo de datos C especificado.  
  
 Este apéndice contiene los siguientes temas.  
  
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
  
 Para obtener una explicación de los tipos de datos ODBC, vea [Tipos de datos en ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md). Para obtener información acerca de los tipos de datos SQL específicos del controlador, consulte la documentación del controlador.
