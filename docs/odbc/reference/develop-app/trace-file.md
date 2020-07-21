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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ddd0ee24649592cf4a1a296a51404334145a3bab
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298062"
---
# <a name="trace-file"></a>Archivo de seguimiento
Una aplicación especifica el archivo de seguimiento estableciendo **la palabra clave** de seguimiento en la entrada del registro ODBC. ini o llamando a **SQLSetConnectAttr** con el atributo de conexión SQL_ATTR_TRACEFILE. Si el archivo no existe cuando el seguimiento está habilitado, el administrador de controladores creará el archivo. Cada aplicación debe tener su propio archivo de seguimiento dedicado para evitar la contención. Una aplicación puede utilizar más de un archivo de seguimiento; el programa de instalación de una aplicación puede proporcionar al usuario una selección de archivos de seguimiento. Si el seguimiento está habilitado dinámicamente, una aplicación también puede mostrar los resultados del seguimiento, en lugar de registrarlos en el archivo de seguimiento.  
  
 El archivo de seguimiento proporciona un registro de cada llamada a función ODBC con los tipos de datos y los valores de todos los argumentos. Registra todas las funciones de entrada y registra todas las funciones devueltas con los códigos de retorno y los Estados de error.  
  
 En ODBC *3. x*, los parámetros de las funciones de conexión no se proporcionan a la dll de seguimiento.
