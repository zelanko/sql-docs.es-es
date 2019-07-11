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
manager: craigg
ms.openlocfilehash: 8138a0cef3a28d31242a74162f0024e28e8b8fe9
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793928"
---
# <a name="trace-file"></a>Archivo de seguimiento
Una aplicación que especifica el archivo de seguimiento estableciendo el **TraceFile** palabra clave en la entrada de registro del archivo Odbc.ini o mediante una llamada a **SQLSetConnectAttr** con el atributo de conexión SQL_ATTR_TRACEFILE. Si el archivo no existe cuando se habilita el seguimiento, el Administrador de controladores creará el archivo. Cada aplicación debe tener su propio archivo de seguimiento dedicado para evitar la contención. Una aplicación puede usar más de un archivo de seguimiento; programa de instalación de la aplicación puede proporcionar al usuario una opción de archivos de seguimiento. Si el seguimiento está habilitado de forma dinámica, una aplicación también puede mostrar los resultados de seguimiento, en lugar de registro en el archivo de seguimiento.  
  
 El archivo de seguimiento proporciona un registro de cada llamada de función ODBC con los tipos de datos y los valores de todos los argumentos. Registra todas las entradas de las funciones y los registros de todas las funciones devueltas con códigos de retorno y los Estados de error.  
  
 En ODBC *3.x*, no se proporcionan parámetros a las funciones de la conexión a la DLL de traza.
