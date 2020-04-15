---
title: Dll de traducción ( Translation DLLs) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3dad12bcd71434c1013b4fde5b4bd0231e56016f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297950"
---
# <a name="translation-dlls"></a>Archivos DLL de traducción
La aplicación y el origen de datos a menudo almacenan datos en diferentes conjuntos de caracteres. ODBC proporciona un mecanismo genérico que permite al controlador traducir datos de un juego de caracteres a otro. Consta de un archivo DLL que implementa las funciones de traducción **SQLDriverToDataSource** y **SQLDataSourceToDriver**, a las que llama el controlador para traducir todos los datos que fluyen entre el origen de datos y el controlador. Este archivo DLL puede ser escrito por el desarrollador de la aplicación, el desarrollador del controlador o un tercero.  
  
 El archivo DLL de traducción para un origen de datos determinado se puede especificar en la información del sistema para ese origen de datos; Para obtener más información, consulte Subclaves de [especificación](../../../odbc/reference/install/data-source-specification-subkeys.md)de origen de datos . También se puede establecer en tiempo de ejecución con los atributos de conexión SQL_ATTR_TRANSLATE_DLL y SQL_ATTR_TRANSLATE_OPTION.  
  
 La opción de traducción es un valor que solo puede ser interpretado por un archivo DLL de traducción determinado. Por ejemplo, si el archivo DLL de traducción se traduce entre diferentes páginas de códigos, la opción podría proporcionar los números de las páginas de códigos utilizadas por la aplicación y el origen de datos. No hay ningún requisito para que un archivo DLL de traducción utilice una opción de traducción.  
  
 Una vez que se ha especificado un archivo DLL de traducción, el controlador lo carga y lo llama para traducir todos los datos que fluyen entre la aplicación y el origen de datos. Esto incluye todas las instrucciones SQL y los parámetros de caracteres que se envían al origen de datos y todos los resultados de caracteres, metadatos de caracteres como nombres de columna y mensajes de error recuperados del origen de datos. Los datos de conexión no se traducen, porque el archivo DLL de traducción no se carga hasta después de que la aplicación se haya conectado al origen de datos.
