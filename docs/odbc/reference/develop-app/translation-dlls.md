---
title: Archivos DLL de traducción | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: ec1d0e23019f3e5b68ad38711c1f041b160ceb31
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63305748"
---
# <a name="translation-dlls"></a>Archivos DLL de traducción
La aplicación y el origen de datos a menudo almacenan datos en diferentes conjuntos de caracteres. ODBC proporciona un mecanismo genérico que permite al controlador traducir datos de un juego de caracteres a otro. Consta de un archivo DLL que implementa las funciones de traducción **SQLDriverToDataSource** y **SQLDataSourceToDriver**, que llama el controlador traduzca todos los datos que fluyen entre el origen de datos y el controlador. Este archivo DLL puede escribirse mediante el programador de aplicaciones, el desarrollador del controlador o un tercero.  
  
 El archivo DLL de traducción para un origen de datos determinado se puede especificar la información del sistema de ese origen de datos; Para obtener más información, consulte [subclaves de especificación del origen de datos](../../../odbc/reference/install/data-source-specification-subkeys.md). También puede establecerse en tiempo de ejecución con los atributos de conexión SQL_ATTR_TRANSLATE_DLL y SQL_ATTR_TRANSLATE_OPTION.  
  
 La opción de conversión es un valor que se puede interpretar sólo mediante una archivo DLL de traducción determinada. Por ejemplo, si la traducción DLL traduce entre páginas de códigos diferentes, la opción puede dar a los números de las páginas de códigos utilizados por la aplicación y el origen de datos. No hay ningún requisito para un archivo DLL de traducción para usar una opción de traducción.  
  
 Después de una traducción que se ha especificado el archivo DLL, el controlador lo carga y lo llama para convertir todos los datos que fluyen entre la aplicación y el origen de datos. Esto incluye todas las instrucciones SQL y parámetros de caracteres que se envían al origen de datos y todos los caracteres resultantes, los metadatos de caracteres como nombres de columna y los mensajes de error que se recuperan del origen de datos. No se traducen los datos de conexión, porque no está cargado el archivo DLL de traducción hasta después de la aplicación se conecta al origen de datos.
