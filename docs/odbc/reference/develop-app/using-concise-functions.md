---
title: Uso de funciones concisas | Documentos de Microsoft
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
- concise functions [ODBC]
- functions [ODBC], concise functions
- descriptors [ODBC], concise functions
ms.assetid: 31ac070f-8c59-4fd5-bd5a-466bb27dbca0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 84e1a884406e4060b957279078b8bfb106b92661
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="using-concise-functions"></a>Uso de funciones concisas
Algunas funciones ODBC obtienen acceso implícito a descriptores. Escritores de aplicaciones pueden resultar más conveniente que llamar a **SQLSetDescField** o **SQLGetDescField**. Estas funciones se denominan *concisa* funciones ya que realizan una serie de funciones, incluidas establecer u obtener los campos de descriptor. Algunas funciones concisas permiten a una aplicación establecer o recuperar varios campos de descriptor relacionados en una única llamada de función.  
  
 Puede llamar a funciones concisas sin primero recupera un identificador de descriptor para su uso como un argumento. Estas funciones de trabajo con los campos de descriptor asociados con el identificador de instrucción que se les llama en.  
  
 Las funciones concisas **SQLBindCol** y **SQLBindParameter** enlazar una columna o parámetro estableciendo los campos de descriptor que corresponden a sus argumentos. Cada una de estas funciones realiza más tareas que simplemente establecer descriptores. **SQLBindCol** y **SQLBindParameter** proporciona una especificación completa del enlace de una columna de datos o el parámetro dinámico. Una aplicación sin embargo, puede cambiar los detalles individuales de un enlace mediante una llamada a **SQLSetDescField** o **SQLSetDescRec** y completamente puede enlazar una columna o parámetro mediante la realización de una serie de llamadas adecuadas para Estas funciones.  
  
 Las funciones concisas **SQLColAttribute**, **SQLDescribeCol**, **SQLDescribeParam**, **SQLNumParams**, y  **SQLNumResultCols** recuperar valores de campos de descriptor.  
  
 **SQLSetDescRec** y **SQLGetDescRec** son funciones concisas que, con una llamada, establecer u obtener varios campos de descriptor que afectan al tipo de datos y el almacenamiento de datos de columna o parámetro. **SQLSetDescRec** es una forma eficaz para cambiar el enlace de datos de columna o parámetro en un solo paso.  
  
 **SQLSetStmtAttr** y **SQLGetStmtAttr** actúan como funciones concisas en algunos casos. (Consulte [campos de Descriptor](../../../odbc/reference/develop-app/descriptor-fields.md).)
