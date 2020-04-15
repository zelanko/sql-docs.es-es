---
title: Uso de funciones concisas ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- concise functions [ODBC]
- functions [ODBC], concise functions
- descriptors [ODBC], concise functions
ms.assetid: 31ac070f-8c59-4fd5-bd5a-466bb27dbca0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 63313e3dfaec8dbcd91f3bb084bbaab46da40c6e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306786"
---
# <a name="using-concise-functions"></a>Uso de funciones concisas
Algunas funciones ODBC obtienen acceso implícito a los descriptores. Los escritores de aplicaciones pueden encontrarlos más convenientes que llamar a **SQLSetDescField** o **SQLGetDescField**. Estas funciones se denominan funciones *concisas* porque realizan una serie de funciones, incluida la configuración o la obtención de campos descriptores. Algunas funciones concisas permiten que una aplicación establezca o recupere varios campos descriptores relacionados en una sola llamada de función.  
  
 Se puede llamar a funciones concisas sin recuperar primero un identificador de descriptor para su uso como argumento. Estas funciones funcionan con los campos descriptores asociados con el identificador de instrucción en el que se llaman.  
  
 Las funciones concisas **SQLBindCol** y **SQLBindParameter** enlazan una columna o parámetro estableciendo los campos descriptores que corresponden a sus argumentos. Cada una de estas funciones realiza más tareas que simplemente establecer descriptores. **SQLBindCol** y **SQLBindParameter** proporcionan una especificación completa del enlace de una columna de datos o parámetro dinámico. Sin embargo, una aplicación puede cambiar los detalles individuales de un enlace llamando a **SQLSetDescField** o **SQLSetDescRec** y puede enlazar completamente una columna o parámetro realizando una serie de llamadas adecuadas a estas funciones.  
  
 Las funciones concisas **SQLColAttribute**, **SQLDescribeCol**, **SQLDescribeParam**, **SQLNumParams**y **SQLNumResultCols** recuperan valores en campos descriptores.  
  
 **SQLSetDescRec** y **SQLGetDescRec** son funciones concisas que, con una llamada, establecen u obtienen varios campos descriptores que afectan al tipo de datos y al almacenamiento de datos de columna o parámetro. **SQLSetDescRec** es una forma eficaz de cambiar el enlace de datos de columna o parámetro en un paso.  
  
 **SQLSetStmtAttr** y **SQLGetStmtAttr** sirven como funciones concisas en algunos casos. (Consulte [Campos descriptores](../../../odbc/reference/develop-app/descriptor-fields.md).)
