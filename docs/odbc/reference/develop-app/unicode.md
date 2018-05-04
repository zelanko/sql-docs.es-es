---
title: Unicode | Documentos de Microsoft
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
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC]
- Unicode [ODBC], about Unicode
ms.assetid: 113e1c9a-8333-4805-86f2-e4b57ab816a5
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db3f4cd59ee69a57e735a875f3ee59f4836ed7a6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="unicode"></a>Unicode
Unicode define la codificación de caracteres en varios idiomas.  
  
 Para obtener más información sobre el estándar Unicode, vea [consorcio Unicode](http://www.unicode.org).  
  
 Unicode define un conjunto de caracteres universales. Una página de códigos ANSI de Windows define un juego de caracteres, que normalmente contiene caracteres para un idioma. Puede ser más difícil de escribir una aplicación que se necesita para usar páginas de códigos diferentes.  
  
 Unicode no requiere una página de códigos. Cada punto de código se asigna a un único carácter en un lenguaje.  
  
 Actualmente, la codificación que es compatible con ODBC de Unicode única es UCS-2, que utiliza un entero de 16 bits (longitud fija) para representar un carácter. Unicode permite a las aplicaciones funcionan en diferentes idiomas.  
  
 El Administrador de controladores ODBC 3.5 (o superior) está habilitada para Unicode. Esto afecta a dos áreas principales: llamadas a funciones y tipos de datos de cadena. Los argumentos de la cadena de función de administrador de controladores mapas y datos de cadena según sea necesario por la aplicación y el controlador, ambos de los cuales pueden ser habilitada para Unicode o ANSI habilitados. Estas dos áreas se describen en detalle en las secciones, [argumentos de la función Unicode](../../../odbc/reference/develop-app/unicode-function-arguments.md) y [datos Unicode](../../../odbc/reference/develop-app/unicode-data.md).  
  
 El Administrador de controladores ODBC 3.5 (o superior) admite el uso de un controlador de Unicode con una aplicación Unicode y una aplicación de ANSI. También admite el uso de un controlador de ANSI con una aplicación de ANSI. El Administrador de controladores proporciona asignación de Unicode a ANSI limitado para una aplicación de Unicode trabajar con un controlador de ANSI.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Argumentos de función de Unicode](../../../odbc/reference/develop-app/unicode-function-arguments.md)  
  
-   [Datos Unicode](../../../odbc/reference/develop-app/unicode-data.md)
