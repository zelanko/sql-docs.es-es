---
title: Unicode | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC]
- Unicode [ODBC], about Unicode
ms.assetid: 113e1c9a-8333-4805-86f2-e4b57ab816a5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1e6201b83b909573476b043cdb1a10543f894def
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62632552"
---
# <a name="unicode"></a>Unicode
Unicode define la codificación de caracteres en varios idiomas.  
  
 Para obtener más información sobre el estándar Unicode, vea [The Unicode Consortium](https://www.unicode.org).  
  
 Unicode define un conjunto de caracteres universales. Una página de códigos ANSI de Windows define un juego de caracteres, que normalmente contiene caracteres para un idioma. Puede ser más difícil de escribir una aplicación que se requiere para usar páginas de códigos diferentes.  
  
 Unicode no requiere una página de códigos. Cada punto de código se asigna a un único carácter en algún lenguaje.  
  
 Actualmente, la codificación que es compatible con ODBC de Unicode única es UCS-2, que utiliza un entero de 16 bits (longitud fija) para representar un carácter. Unicode permite que las aplicaciones funcionan en diferentes idiomas.  
  
 El Administrador de controladores ODBC 3.5 (o posterior) está habilitada para Unicode. Esto afecta a dos áreas principales: llamadas a funciones y tipos de datos de cadena. Los argumentos de cadena de función de administrador de controladores mapas y datos de cadena según sea necesario por la aplicación y el controlador, ambos de los cuales pueden ser compatibles con Unicode o habilitada para ANSI. Estas dos áreas se describen en detalle en las secciones, [argumentos de la función Unicode](../../../odbc/reference/develop-app/unicode-function-arguments.md) y [datos Unicode](../../../odbc/reference/develop-app/unicode-data.md).  
  
 El Administrador de controladores ODBC 3.5 (o posterior) admite el uso de un controlador de Unicode con una aplicación Unicode y una aplicación de ANSI. También admite el uso de un controlador de ANSI con una aplicación de ANSI. El Administrador de controladores proporciona limitado de Unicode a ANSI asignación para una aplicación Unicode trabajando con un controlador de ANSI.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Argumentos de función de Unicode](../../../odbc/reference/develop-app/unicode-function-arguments.md)  
  
-   [Datos Unicode](../../../odbc/reference/develop-app/unicode-data.md)
