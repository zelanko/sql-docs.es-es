---
description: Identificadores de tipo SQL
title: Identificadores de tipo SQL | Microsoft Docs
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
ms.openlocfilehash: 211cfdbe7805bade2875723a1cb62a02b5c876d3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424517"
---
# <a name="sql-type-identifiers"></a>Identificadores de tipo SQL
Cada origen de datos define sus propios tipos de datos SQL. ODBC define los identificadores de tipo y describe las características generales de los tipos de datos de SQL que podrían estar asignados a cada identificador de tipo. Es específico del controlador el modo en que cada tipo de datos del origen de datos subyacente se asigna a un identificador de tipo SQL de ODBC.  
  
 Por ejemplo, SQL_CHAR es el identificador de tipo de una columna de caracteres con una longitud fija, normalmente de entre 1 y 254 caracteres. Estas características se corresponden con el tipo de datos CHAR que se encuentra en muchos orígenes de datos SQL. Por lo tanto, cuando una aplicación detecta que el identificador de tipo de una columna es SQL_CHAR, puede suponer que probablemente está tratando con una columna CHAR. Sin embargo, todavía debería comprobar la longitud de bytes de la columna antes de suponer que tiene entre 1 y 254 caracteres; por ejemplo, el controlador para un origen de datos que no es de SQL podría asignar una columna de caracteres de longitud fija de 500 caracteres a SQL_CHAR o SQL_LONGVARCHAR, porque ninguna de ellas es una coincidencia exacta.  
  
 ODBC define una gran variedad de identificadores de tipo SQL. Sin embargo, no es necesario que el controlador Use todos estos identificadores. En su lugar, solo usa los identificadores que necesita para exponer los tipos de datos de SQL admitidos por el origen de datos subyacente. Si el origen de datos subyacente admite tipos de datos de SQL a los que no se corresponde ningún identificador de tipo, el controlador puede definir identificadores de tipo adicionales. Para obtener más información, vea [tipos de datos específicos del controlador, tipos de descriptores, tipos de información, tipos de diagnóstico y atributos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
 Para obtener una descripción completa de los identificadores de tipo SQL, vea [tipos de datos de C](../../../odbc/reference/appendixes/c-data-types.md) en el Apéndice D: tipos de datos.
