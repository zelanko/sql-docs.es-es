---
title: Los identificadores de tipo SQL | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1763ee0cd8c5bc2017160de44b9c047781649eba
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63150030"
---
# <a name="sql-type-identifiers"></a>Identificadores de tipo SQL
Cada origen de datos define sus propios tipos de datos SQL. ODBC define los identificadores de tipo y describe las características generales de los tipos de datos SQL que se pueden asignar a cada identificador de tipo. Es cómo cada tipo de datos en el origen de datos subyacente se asigna a un identificador de tipo SQL de ODBC específicos del controlador.  
  
 Por ejemplo, SQL_CHAR es el identificador de tipo para una columna de caracteres con una longitud fija, normalmente entre 1 y 254 caracteres. Estas características se corresponden con el tipo de datos de carácter se encuentra en muchos orígenes de datos SQL. Por lo tanto, cuando una aplicación descubre que el identificador de tipo para una columna SQL_CHAR, puede asumir probablemente se trata de una columna CHAR. Sin embargo, debería comprobar la longitud de bytes de la columna antes de dar por supuesto que está entre 1 y 254 caracteres; el controlador para un origen de datos que no sea de SQL, por ejemplo, podría asignar una columna de caracteres de longitud fija de 500 caracteres SQL_CHAR o SQL_LONGVARCHAR, porque ninguna de ellas es una coincidencia exacta.  
  
 ODBC define una amplia variedad de identificadores de tipo SQL. Sin embargo, el controlador no debe usar todos estos identificadores. En su lugar, usa solo esos identificadores que necesita para exponer los tipos de datos SQL admite el origen de datos subyacente. Si el origen de datos subyacente admite tipos de datos SQL para que ningún identificador de tipo se corresponde, el controlador puede definir los identificadores de tipo adicionales. Para obtener más información, consulte [los tipos de datos específicos del controlador, Descriptor tipos, tipos de información, tipos de diagnóstico y atributos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
 Para obtener una descripción completa de identificadores de tipo SQL, consulte [tipos de datos C](../../../odbc/reference/appendixes/c-data-types.md) en el apéndice D: Tipos de datos.
