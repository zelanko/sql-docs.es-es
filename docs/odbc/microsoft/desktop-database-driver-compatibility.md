---
title: Compatibilidad con controladores de escritorio de la base de datos | Documentos de Microsoft
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
- compatibility [ODBC], Unicode
- Unicode [ODBC], desktop database drivers
- ODBC desktop database drivers [ODBC], Unicode
- backward compatibility [ODBC], Unicode
- desktop database drivers [ODBC], Unicode
- Jet-based ODBC drivers [ODBC], Unicode
ms.assetid: dd695638-1a0b-4e27-8a6a-9510ebb5a5ee
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 557a7254e9cea7476ee3de706da86519f9ef1fec
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="desktop-database-driver-compatibility"></a>Compatibilidad con controladores de escritorio de la base de datos
Unicode es un método de software de codificación de caracteres que trata todos los caracteres que tienen un ancho fijo de dos bytes. Este método se usa como alternativa a la codificación de caracteres ANSI de Windows, que, dado que representa los caracteres de un byte, está limitada a 256 caracteres. Puesto que Unicode puede representar más de 65.000 caracteres, se adapta a muchos idiomas cuyos caracteres no se representan en la codificación ANSI.  
  
 El Administrador de controladores ODBC 3.5 (o posterior) está habilitada para Unicode. Esto afecta a dos áreas principales: llamadas a funciones y tipos de datos de cadena. Los argumentos de la cadena de función de administrador de controladores mapas y datos de cadena según sea necesario por la aplicación y el controlador, ambos de los cuales pueden ser habilitada para Unicode o ANSI habilitados.  
  
 El Administrador de controladores ODBC 3.5 (o posterior) admite el uso de un controlador de Unicode con una aplicación Unicode y una aplicación de ANSI. También admite el uso de un controlador de ANSI con una aplicación de ANSI. El Administrador de controladores proporciona asignación de Unicode a ANSI limitado para una aplicación de Unicode trabajar con un controlador de ANSI. Esto permite el acceso a las bases de datos de Jet 3.5 y soporte técnico de todos los tipos de archivo ISAM existentes.  
  
 Cuando una aplicación ANSI usa el controlador de base de datos ODBC Desktop 4.0 y tiene acceso a Microsoft Access 4.0 o versiones posteriores, el controlador expone el tipo de datos como SQL_CHAR, SQL_VARCHAR o SQL_LONGVARCHAR Aunque Jet 4.0 es compatible con la versión de ancho. Las versiones anteriores de Jet no admiten SQL_WCHAR, SQL_WVARCHAR y SQL_WLONGVARCHAR. Esta restricción también se aplica en los casos donde se use el formato antiguo con el motor de base de datos de Jet 4.0.  
  
 Para obtener más información sobre los problemas de Unicode con ODBC, consulte [Unicode](../../odbc/reference/develop-app/unicode.md) en consideraciones sobre la programación.
