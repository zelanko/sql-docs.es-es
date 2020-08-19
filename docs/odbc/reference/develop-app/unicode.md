---
description: Unicode
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a09a2647175d2b19aa44f1458d0ae8c4ef4565c7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424437"
---
# <a name="unicode"></a>Unicode
Unicode define la codificación de caracteres en muchos idiomas.  
  
 Para obtener más información sobre el estándar Unicode, vea [Unicode Consortium](https://www.unicode.org).  
  
 Unicode define un juego de caracteres universal. Una página de códigos ANSI de Windows define un juego de caracteres que normalmente contiene caracteres para un idioma. Puede ser más difícil escribir una aplicación necesaria para usar páginas de códigos diferentes.  
  
 Unicode no requiere una página de códigos. Cada punto de código se asigna a un único carácter en algún idioma.  
  
 Actualmente, la única codificación Unicode compatible con ODBC es UCS-2, que usa un entero de 16 bits (longitud fija) para representar un carácter. Unicode permite a las aplicaciones trabajar en distintos idiomas.  
  
 El administrador de controladores ODBC 3,5 (o posterior) está habilitado para Unicode. Esto afecta a dos áreas principales: las llamadas de función y los tipos de datos de cadena. El administrador de controladores asigna los argumentos de cadena de función y los datos de cadena según lo requiera la aplicación y el controlador, y ambos pueden estar habilitados para Unicode o ANSI. Estas dos áreas se describen en detalle en las secciones, [argumentos de función Unicode](../../../odbc/reference/develop-app/unicode-function-arguments.md) y [datos Unicode](../../../odbc/reference/develop-app/unicode-data.md).  
  
 El administrador de controladores ODBC 3,5 (o posterior) admite el uso de un controlador Unicode con una aplicación Unicode y una aplicación ANSI. También admite el uso de un controlador ANSI con una aplicación ANSI. El administrador de controladores proporciona una asignación de Unicode a ANSI limitada para una aplicación Unicode que trabaja con un controlador ANSI.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Argumentos de función de Unicode](../../../odbc/reference/develop-app/unicode-function-arguments.md)  
  
-   [Datos Unicode](../../../odbc/reference/develop-app/unicode-data.md)
