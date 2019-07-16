---
title: Archivo de seguimiento | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c94c3718c116b37eb198264887dfb4a319bd1dc3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985151"
---
# <a name="trace-file"></a>Archivo de seguimiento
Una aplicación que especifica el archivo de seguimiento estableciendo el **TraceFile** palabra clave en la entrada de registro del archivo Odbc.ini o mediante una llamada a **SQLSetConnectAttr** con el atributo de conexión SQL_ATTR_TRACEFILE. Si el archivo no existe cuando se habilita el seguimiento, el Administrador de controladores creará el archivo. Cada aplicación debe tener su propio archivo de seguimiento dedicado para evitar la contención. Una aplicación puede usar más de un archivo de seguimiento; programa de instalación de la aplicación puede proporcionar al usuario una opción de archivos de seguimiento. Si el seguimiento está habilitado de forma dinámica, una aplicación también puede mostrar los resultados de seguimiento, en lugar de registro en el archivo de seguimiento.  
  
 El archivo de seguimiento proporciona un registro de cada llamada de función ODBC con los tipos de datos y los valores de todos los argumentos. Registra todas las entradas de las funciones y los registros de todas las funciones devueltas con códigos de retorno y los Estados de error.  
  
 En ODBC *3.x*, no se proporcionan parámetros a las funciones de la conexión a la DLL de traza.
