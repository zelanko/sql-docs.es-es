---
title: Archivos DLL de traducción | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- translation DLLs [ODBC]
ms.assetid: 38975059-b346-410f-bb27-326f3f7bbf39
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7ab283e0086afadd5fc5bbd9e465241ca997890e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="translation-dlls"></a>Archivos DLL de traducción
La aplicación y el origen de datos suelen almacenan datos en distintos juegos de caracteres. ODBC proporciona un mecanismo genérico que permite al controlador traducir datos de un juego de caracteres a otro. Consta de un archivo DLL que implementa las funciones de traducción **SQLDriverToDataSource** y **SQLDataSourceToDriver**, que se llama por el controlador traduzca todos los datos que fluyen entre el origen de datos y el controlador. Este archivo DLL puede ser escrita por el desarrollador de la aplicación, el desarrollador del controlador o un tercero.  
  
 El archivo DLL de traducción para un origen de datos determinado se puede especificar en la información del sistema para ese origen de datos; Para obtener más información, consulte [subclaves de especificación del origen de datos](../../../odbc/reference/install/data-source-specification-subkeys.md). También puede establecerse en tiempo de ejecución con los atributos de conexión SQL_ATTR_TRANSLATE_DLL y SQL_ATTR_TRANSLATE_OPTION.  
  
 La opción de conversión es un valor que puede interpretar un archivo DLL de traducción determinada. Por ejemplo, si la traducción DLL traduce entre páginas de códigos distintas, la opción puede dar a los números de las páginas de códigos utilizados por la aplicación y el origen de datos. No hay ningún requisito para un archivo DLL de traducción que usen una opción de traducción.  
  
 Después de una traducción que se ha especificado el archivo DLL, el controlador lo carga y lo llama para traducir los datos entre la aplicación y el origen de datos. Esto incluye todas las instrucciones SQL y parámetros de caracteres que se envían al origen de datos y todos los caracteres resultantes, los metadatos de caracteres como nombres de columna y los mensajes de error que se recuperan del origen de datos. Datos de conexión no se traducen, porque el archivo DLL de traducción no se ha cargado hasta después de la aplicación se ha conectado al origen de datos.
