---
title: Archivo de seguimiento (Trace File) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- trace files [ODBC]
- tracing options [ODBC], trace files
ms.assetid: ec97f949-126f-40a2-b67e-e74520a524cb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ddd0ee24649592cf4a1a296a51404334145a3bab
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298062"
---
# <a name="trace-file"></a>Archivo de seguimiento
Una aplicación especifica el archivo de seguimiento estableciendo el **TraceFile** palabra clave en el Odbc.ini entrada del Registro o mediante una llamada a **SQLSetConnectAttr** con el SQL_ATTR_TRACEFILE atributo de conexión. Si el archivo no existe cuando se habilita el seguimiento, el Administrador de controladores creará el archivo. Cada aplicación debe tener su propio archivo de seguimiento dedicado para evitar la contención. Una aplicación puede utilizar más de un archivo de seguimiento; el programa de instalación de una aplicación puede proporcionar al usuario una selección de archivos de seguimiento. Si el seguimiento está habilitado dinámicamente, una aplicación también puede mostrar los resultados de seguimiento, en lugar de registrar en el archivo de seguimiento.  
  
 El archivo de seguimiento proporciona un registro de cada llamada de función ODBC con los tipos de datos y los valores de todos los argumentos. Registra todas las funciones de entrada y registra todas las funciones devueltas con códigos de retorno y estados de error.  
  
 En ODBC *3.x*, los parámetros de las funciones de conexión no se proporcionan al archivo DLL de seguimiento.
