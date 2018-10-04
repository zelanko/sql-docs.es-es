---
title: Uso de funciones concisas | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d70d3ca60a046a355549260406edba261f805e4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47722733"
---
# <a name="using-concise-functions"></a>Uso de funciones concisas
Algunas funciones ODBC obtienen acceso implícito a descriptores. Los escritores de aplicaciones pueden encontrarlos más conveniente que llamar a **SQLSetDescField** o **SQLGetDescField**. Estas funciones se denominan *concisa* funciona puesto que realizan una serie de funciones, incluido establecer u obtener los campos de descriptor. Algunas funciones concisas, permitir que una aplicación establecer o recuperar varios campos de descriptor relacionados en una única llamada de función.  
  
 Funciones concisas se pueden llamar sin primero recupera un identificador de descriptor para su uso como un argumento. Estas funciones funcionan con los campos de descriptor asociados con el identificador de instrucción que se les llama en.  
  
 Las funciones concisas **SQLBindCol** y **SQLBindParameter** enlazar una columna o parámetro estableciendo los campos de descriptor que corresponden a sus argumentos. Cada una de estas funciones realiza más tareas que basta con establecer descriptores. **SQLBindCol** y **SQLBindParameter** proporcionan una especificación completa del enlace de una columna de datos o un parámetro dinámico. Una aplicación sin embargo, puede cambiar los detalles individuales de un enlace mediante una llamada a **SQLSetDescField** o **SQLSetDescRec** y completamente puede enlazar una columna o parámetro mediante la realización de una serie de llamadas adecuadas para Estas funciones.  
  
 Las funciones concisas **SQLColAttribute**, **SQLDescribeCol**, **SQLDescribeParam**, **SQLNumParams**, y  **SQLNumResultCols** recuperar los valores en campos de descriptor.  
  
 **SQLSetDescRec** y **SQLGetDescRec** son funciones concisas que, con una llamada, establecer u obtención varios campos de descriptor que afectan al tipo de datos y almacenamiento de datos de columna o parámetro. **SQLSetDescRec** es una forma eficaz para cambiar el enlace de datos de columna o parámetro en un solo paso.  
  
 **SQLSetStmtAttr** y **SQLGetStmtAttr** actuar como funciones concisas, en algunos casos. (Consulte [campos de Descriptor](../../../odbc/reference/develop-app/descriptor-fields.md).)
