---
title: Compatibilidad de controladores de bases de datos de escritorio | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], Unicode
- Unicode [ODBC], desktop database drivers
- ODBC desktop database drivers [ODBC], Unicode
- backward compatibility [ODBC], Unicode
- desktop database drivers [ODBC], Unicode
- Jet-based ODBC drivers [ODBC], Unicode
ms.assetid: dd695638-1a0b-4e27-8a6a-9510ebb5a5ee
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89eea7ab112eaefdc73c7cbc72ee3555797c7efd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303526"
---
# <a name="desktop-database-driver-compatibility"></a>Compatibilidad con controladores de escritorio de la base de datos
Unicode es un método de codificación de caracteres de software que trata todos los caracteres como si tuvieran un ancho fijo de dos bytes. Este método se usa como alternativa a la codificación de caracteres ANSI de Windows, que, dado que representa los caracteres de un byte, está limitado a 256 caracteres. Dado que Unicode puede representar más de 65.000 caracteres, admite muchos idiomas cuyos caracteres no se representan en codificación ANSI.  
  
 El administrador de controladores ODBC 3,5 (o posterior) está habilitado para Unicode. Esto afecta a dos áreas principales: las llamadas de función y los tipos de datos de cadena. El administrador de controladores asigna los argumentos de cadena de función y los datos de cadena según lo requiera la aplicación y el controlador, y ambos pueden estar habilitados para Unicode o ANSI.  
  
 El administrador de controladores ODBC 3,5 (o posterior) admite el uso de un controlador Unicode con una aplicación Unicode y una aplicación ANSI. También admite el uso de un controlador ANSI con una aplicación ANSI. El administrador de controladores proporciona una asignación de Unicode a ANSI limitada para una aplicación Unicode que trabaja con un controlador ANSI. Esto permite el acceso a las bases de datos Jet 3,5 y la compatibilidad de todos los tipos de archivo ISAM existentes.  
  
 Cuando una aplicación ANSI usa el controlador de base de datos de escritorio ODBC 4,0 y obtiene acceso a Microsoft Access 4,0 o posterior, el controlador expone el tipo de datos como SQL_CHAR, SQL_VARCHAR o SQL_LONGVARCHAR, aunque jet 4,0 admita la versión ancha. Las versiones anteriores de Jet no admiten SQL_WCHAR, SQL_WVARCHAR y SQL_WLONGVARCHAR. Esta restricción también se aplica en los casos en los que se usan los formatos antiguos con el Motor de base de datos de jet 4,0.  
  
 Para obtener más información sobre los problemas de Unicode con ODBC, vea [Unicode](../../odbc/reference/develop-app/unicode.md) en consideraciones de programación.
