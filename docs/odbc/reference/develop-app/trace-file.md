---
title: Archivo de seguimiento | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- trace files [ODBC]
- tracing options [ODBC], trace files
ms.assetid: ec97f949-126f-40a2-b67e-e74520a524cb
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 17820a03e062feb24e3b10e58cbcf29b3feb8ba3
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="trace-file"></a>Archivo de seguimiento
Una aplicación que especifica el archivo de seguimiento estableciendo el **TraceFile** palabra clave en la entrada de registro Odbc.ini o mediante una llamada a **SQLSetConnectAttr** con el atributo de conexión SQL_ATTR_TRACEFILE. Si el archivo no existe cuando se habilita el seguimiento, el Administrador de controladores creará el archivo. Cada aplicación debe tener su propio archivo de seguimiento dedicado para evitar la contención. Una aplicación puede utilizar más de un archivo de seguimiento; programa de instalación de una aplicación puede proporcionar al usuario con una variedad de archivos de seguimiento. Si se habilita el seguimiento dinámicamente, una aplicación también puede mostrar los resultados de seguimiento, en lugar de registro en el archivo de seguimiento.  
  
 El archivo de seguimiento proporciona un registro de cada llamada de función ODBC con los tipos de datos y los valores de todos los argumentos. Registra todas las funciones y registra todas las funciones devueltas con códigos de retorno y Estados de error.  
  
 En ODBC 3*.x*, no se proporcionan parámetros a las funciones de conexión en el archivo DLL de seguimiento.
