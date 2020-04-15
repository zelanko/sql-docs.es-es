---
title: Unicode Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9824e76cebabb6f5f84505292801a0094e359f0f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302452"
---
# <a name="unicode"></a>Unicode
Unicode define la codificación de caracteres en muchos idiomas.  
  
 Para obtener más información sobre el estándar Unicode, consulte [The Unicode Consortium](https://www.unicode.org).  
  
 Unicode define un juego de caracteres universal. Una página de códigos ANSI de Windows define un juego de caracteres, que normalmente contiene caracteres para un idioma. Puede ser más difícil escribir una aplicación que sea necesaria para usar diferentes páginas de códigos.  
  
 Unicode no requiere una página de códigos. Cada punto de código se asigna a un solo carácter en algún idioma.  
  
 Actualmente, la única codificación Unicode que ODBC admite es UCS-2, que utiliza un entero de 16 bits (longitud fija) para representar un carácter. Unicode permite que las aplicaciones funcionen en diferentes idiomas.  
  
 El Administrador de controladores ODBC 3.5 (o superior) está habilitado para Unicode. Esto afecta a dos áreas principales: llamadas a funciones y tipos de datos de cadena. El Administrador de controladores asigna argumentos de cadena de función y datos de cadena según lo requieran la aplicación y el controlador, los cuales pueden estar habilitados para Unicode o ANSI. Estas dos áreas se describen en detalle en las [secciones, Argumentos](../../../odbc/reference/develop-app/unicode-function-arguments.md) de función Unicode y [Datos Unicode](../../../odbc/reference/develop-app/unicode-data.md).  
  
 El Administrador de controladores ODBC 3.5 (o superior) admite el uso de un controlador Unicode con una aplicación Unicode y una aplicación ANSI. También admite el uso de un controlador ANSI con una aplicación ANSI. El Administrador de controladores proporciona una asignación limitada de Unicode a ANSI para una aplicación Unicode que trabaja con un controlador ANSI.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Argumentos de función de Unicode](../../../odbc/reference/develop-app/unicode-function-arguments.md)  
  
-   [Datos Unicode](../../../odbc/reference/develop-app/unicode-data.md)
