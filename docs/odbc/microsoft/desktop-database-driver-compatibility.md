---
title: Compatibilidad de controladores de escritorio de la base de datos | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d081d53458ec59eb2ac9f05c5c1d47d6991b5010
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63240355"
---
# <a name="desktop-database-driver-compatibility"></a>Compatibilidad con controladores de escritorio de la base de datos
Unicode es un método software de codificación de caracteres que trata todos los caracteres con un ancho fijo de dos bytes. Este método se utiliza como una alternativa a la codificación de caracteres ANSI de Windows, que, dado que representa los caracteres de un byte, está limitada a 256 caracteres. Dado que Unicode puede representar más de 65.000 caracteres, se adapta a los muchos lenguajes cuyos caracteres no están representadas en la codificación ANSI.  
  
 El Administrador de controladores ODBC 3.5 (o posterior) está habilitada para Unicode. Esto afecta a dos áreas principales: llamadas a funciones y tipos de datos de cadena. Los argumentos de cadena de función de administrador de controladores mapas y datos de cadena según sea necesario por la aplicación y el controlador, ambos de los cuales pueden ser compatibles con Unicode o habilitada para ANSI.  
  
 El Administrador de controladores ODBC 3.5 (o posterior) admite el uso de un controlador de Unicode con una aplicación Unicode y una aplicación de ANSI. También admite el uso de un controlador de ANSI con una aplicación de ANSI. El Administrador de controladores proporciona limitado de Unicode a ANSI asignación para una aplicación Unicode trabajando con un controlador de ANSI. Esto permite el acceso a la compatibilidad de todos los tipos de archivo ISAM existentes y las bases de datos Jet 3.5.  
  
 Cuando una aplicación ANSI usa el controlador de base de datos ODBC Desktop 4.0 y tiene acceso a Microsoft Access 4.0 o versiones posteriores, el controlador expone el tipo de datos como SQL_CHAR, SQL_VARCHAR o SQL_LONGVARCHAR Aunque Jet 4.0 es compatible con la versión de ancho. Las versiones anteriores de Jet no admiten SQL_WCHAR, SQL_WVARCHAR y SQL_WLONGVARCHAR. Esta restricción también se aplica en los casos donde se utiliza el formato anterior con el motor de base de datos de Jet 4.0.  
  
 Para obtener más información sobre los problemas de Unicode con ODBC, consulte [Unicode](../../odbc/reference/develop-app/unicode.md) en consideraciones sobre la programación.
