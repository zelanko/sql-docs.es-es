---
title: Compatibilidad de controladores de base de datos de escritorio ? Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303526"
---
# <a name="desktop-database-driver-compatibility"></a>Compatibilidad con controladores de escritorio de la base de datos
Unicode es un método de codificación de caracteres de software que trata todos los caracteres como tener un ancho fijo de dos bytes. Este método se utiliza como alternativa a la codificación de caracteres ANSI de Windows, que, dado que representa caracteres en un byte, está limitada a 256 caracteres. Dado que Unicode puede representar más de 65.000 caracteres, admite muchos idiomas cuyos caracteres no están representados en la codificación ANSI.  
  
 El Administrador de controladores ODBC 3.5 (o posterior) está habilitado para Unicode. Esto afecta a dos áreas principales: llamadas a funciones y tipos de datos de cadena. El Administrador de controladores asigna argumentos de cadena de función y datos de cadena según lo requieran la aplicación y el controlador, los cuales pueden estar habilitados para Unicode o ANSI.  
  
 El Administrador de controladores ODBC 3.5 (o posterior) admite el uso de un controlador Unicode con una aplicación Unicode y una aplicación ANSI. También admite el uso de un controlador ANSI con una aplicación ANSI. El Administrador de controladores proporciona una asignación limitada de Unicode a ANSI para una aplicación Unicode que trabaja con un controlador ANSI. Esto permite el acceso a las bases de datos de Jet 3.5 y la compatibilidad con todos los tipos de archivos ISAM existentes.  
  
 Cuando una aplicación ANSI utiliza el controlador de base de datos de escritorio ODBC 4.0 y tiene acceso a Microsoft Access 4.0 o posterior, el controlador expone el tipo de datos como SQL_CHAR, SQL_VARCHAR o SQL_LONGVARCHAR aunque Jet 4.0 admita la versión amplia. Las versiones anteriores de Jet no admiten SQL_WCHAR, SQL_WVARCHAR y SQL_WLONGVARCHAR. Esta restricción también se aplica en los casos en que los formatos antiguos se utilizan con el motor de base de datos Jet 4.0.  
  
 Para obtener más información acerca de los problemas Unicode con ODBC, consulte [Unicode](../../odbc/reference/develop-app/unicode.md) en Consideraciones de programación.
