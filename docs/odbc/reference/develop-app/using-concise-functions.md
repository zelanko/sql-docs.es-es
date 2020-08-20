---
description: Uso de funciones concisas
title: Usar funciones concisas | Microsoft Docs
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
ms.openlocfilehash: b0dcd16c1380c95921d5e4bb58831e2dd939ecf1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482801"
---
# <a name="using-concise-functions"></a>Uso de funciones concisas
Algunas funciones ODBC obtienen acceso implícito a los descriptores. Los escritores de aplicaciones pueden encontrarlos más cómodos que llamar a **SQLSetDescField** o **SQLGetDescField**. Estas funciones se denominan funciones *concisas* porque realizan una serie de funciones, incluida la configuración u obtención de campos de descriptor. Algunas funciones concisas permiten a una aplicación establecer o recuperar varios campos descriptores relacionados en una única llamada de función.  
  
 Se puede llamar a las funciones concisas sin recuperar primero un identificador de descriptor para su uso como argumento. Estas funciones funcionan con los campos de descriptor asociados al identificador de instrucción en el que se les llama.  
  
 Las funciones concisas **SQLBindCol** y **SQLBindParameter** enlazan una columna o un parámetro estableciendo los campos de descriptor que corresponden a sus argumentos. Cada una de estas funciones realiza más tareas que simplemente la configuración de descriptores. **SQLBindCol** y **SQLBindParameter** proporcionan una especificación completa del enlace de una columna de datos o un parámetro dinámico. Sin embargo, una aplicación puede cambiar los detalles individuales de un enlace llamando a **SQLSetDescField** o **SQLSetDescRec** y puede enlazar completamente una columna o un parámetro mediante la realización de una serie de llamadas adecuadas a estas funciones.  
  
 Las funciones concisas **SQLColAttribute**, **SQLDescribeCol**, **SQLDescribeParam**, **SQLNumParams**y **SQLNumResultCols** recuperan valores en los campos de descriptor.  
  
 **SQLSetDescRec** y **SQLGetDescRec** son funciones concisas que, con una llamada, establecen u obtienen varios campos de descriptor que afectan al tipo de datos y al almacenamiento de datos de parámetros o columnas. **SQLSetDescRec** es una manera eficaz de cambiar el enlace de datos de columnas o parámetros en un solo paso.  
  
 **SQLSetStmtAttr** y **SQLGetStmtAttr** sirven como funciones concisas en algunos casos. (Consulte [campos descriptores](../../../odbc/reference/develop-app/descriptor-fields.md)).
