---
title: Identificadores de tipo SQL ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- SQL data types [ODBC], identifiers
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: 22f6793b-2f43-4281-b35a-28f48e504dd8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 95bf46844e9ed91aac1ec6cb93a298995f0901d6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299775"
---
# <a name="sql-type-identifiers"></a>Identificadores de tipo SQL
Cada origen de datos define sus propios tipos de datos SQL. ODBC define identificadores de tipo y describe las características generales de los tipos de datos SQL que se pueden asignar a cada identificador de tipo. Es específico del controlador cómo cada tipo de datos en el origen de datos subyacente se asigna a un identificador de tipo SQL de ODBC.  
  
 Por ejemplo, SQL_CHAR es el identificador de tipo de una columna de caracteres con una longitud fija, normalmente entre 1 y 254 caracteres. Estas características corresponden al tipo de datos CHAR que se encuentra en muchos orígenes de datos SQL. Por lo tanto, cuando una aplicación detecta que el identificador de tipo para una columna es SQL_CHAR, puede suponer que probablemente está tratando con una columna CHAR. Sin embargo, todavía debe comprobar la longitud de bytes de la columna antes de asumir que está entre 1 y 254 caracteres; el controlador de un origen de datos no SQL, por ejemplo, podría asignar una columna de caracteres de longitud fija de 500 caracteres a SQL_CHAR o SQL_LONGVARCHAR, porque ninguno es una coincidencia exacta.  
  
 ODBC define una amplia variedad de identificadores de tipo SQL. Sin embargo, el controlador no es necesario para usar todos estos identificadores. En su lugar, solo usa los identificadores que necesita para exponer los tipos de datos SQL admitidos por el origen de datos subyacente. Si el origen de datos subyacente admite tipos de datos SQL a los que no corresponde ningún identificador de tipo, el controlador puede definir identificadores de tipo adicionales. Para obtener más información, vea [Tipos de datos específicos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)del controlador, Tipos de descriptor, Tipos de información, Tipos de diagnóstico y Atributos .  
  
 Para obtener una descripción completa de los identificadores de tipo SQL, vea Tipos de [datos de C](../../../odbc/reference/appendixes/c-data-types.md) en apéndice D: tipos de datos.
