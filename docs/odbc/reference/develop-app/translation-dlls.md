---
title: Archivos dll de traducción | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translation DLLs [ODBC]
ms.assetid: 38975059-b346-410f-bb27-326f3f7bbf39
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 168b7b5ef6f8b88a39dbbb0942cf1520adf261e6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086034"
---
# <a name="translation-dlls"></a>Archivos DLL de traducción
La aplicación y el origen de datos suelen almacenar los datos en diferentes conjuntos de caracteres. ODBC proporciona un mecanismo genérico que permite al controlador traducir los datos de un juego de caracteres a otro. Consta de un archivo DLL que implementa las funciones de traducción **SQLDriverToDataSource** y **SQLDataSourceToDriver**, a las que llama el controlador para traducir todo el flujo de datos entre el origen de datos y el controlador. El desarrollador de la aplicación, el desarrollador del controlador o un tercero pueden escribir este archivo DLL.  
  
 La DLL de traducción para un origen de datos determinado se puede especificar en la información del sistema para ese origen de datos. para obtener más información, vea [subclaves de especificación de origen de datos](../../../odbc/reference/install/data-source-specification-subkeys.md). También se puede establecer en tiempo de ejecución con los atributos de conexión SQL_ATTR_TRANSLATE_DLL y SQL_ATTR_TRANSLATE_OPTION.  
  
 La opción Translation es un valor que solo puede interpretar un archivo DLL de traducción determinado. Por ejemplo, si el archivo DLL de traducción se traduce entre diferentes páginas de códigos, la opción podría proporcionar los números de las páginas de códigos utilizadas por la aplicación y el origen de datos. No es necesario que un archivo DLL de traducción use una opción de traducción.  
  
 Una vez que se ha especificado un archivo DLL de traducción, el controlador lo carga y lo llama para traducir todo el flujo de datos entre la aplicación y el origen de datos. Esto incluye todas las instrucciones SQL y los parámetros de caracteres que se envían al origen de datos, así como todos los resultados de caracteres, metadatos de caracteres como nombres de columna y mensajes de error recuperados del origen de datos. No se traducen los datos de conexión, ya que la DLL de traducción no se carga hasta que la aplicación se haya conectado al origen de datos.
