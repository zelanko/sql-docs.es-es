---
title: Subclave ODBC | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- registry entries for data sources [ODBC], ODBC subkey
- subkeys [ODBC], ODBC subkey
- ODBC subkey [ODBC]
ms.assetid: f9534144-8f42-4946-b0fb-638e9dcde9c8
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c90ca7ef439d1f12df7ddb18e95dea883b7142af
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-subkey"></a>Subclave ODBC
Los valores bajo la subclave ODBC especifican opciones de seguimiento de ODBC. Estas opciones se establecen a través de la ficha trazas del cuadro de diálogo Administrador de orígenes de datos ODBC muestra **SQLManageDataSources**. La subclave ODBC propio es opcional. El formato de estos valores es como se muestra en la tabla siguiente.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|Seguimiento|REG_SZ|**0** &#124; **1**|  
|TraceFile|REG_SZ|*ruta de acceso de archivo de seguimiento*|  
  
 Los valores tienen los significados que se describen en la tabla siguiente.  
  
|Valor|Significado|  
|-----------|-------------|  
|Seguimiento|Si el valor de seguimiento se establece en 1 cuando una aplicación llama **SQLAllocHandle** con la opción de SQL_HANDLE_ENV, el seguimiento está habilitado para la aplicación que realiza la llamada.<br /><br /> Si la palabra clave de seguimiento se establece en 0 cuando una aplicación llama **SQLAllocHandle** con la opción de SQL_HANDLE_ENV, el seguimiento está deshabilitado para la aplicación que realiza la llamada. Es el valor predeterminado.<br /><br /> Una aplicación puede habilitar o deshabilitar el seguimiento con el atributo de conexión SQL_ATTR_TRACE. Sin embargo, al hacerlo así no cambia los datos para este valor.|  
|TraceFile|Si el seguimiento está habilitado, el Administrador de controladores se escribe en el archivo de seguimiento especificado por el valor del archivo de seguimiento.<br /><br /> Si no se especifica ningún archivo de seguimiento, el Administrador de controladores se escribe en el archivo Sql.log en la unidad actual. Es el valor predeterminado.<br /><br /> El seguimiento debe usarse solo para una sola aplicación, o cada aplicación debe especificar un archivo de seguimiento diferente. De lo contrario, dos o más aplicaciones intentará abrir el mismo archivo de seguimiento al mismo tiempo, produciendo un error.<br /><br /> Una aplicación puede especificar un nuevo archivo de seguimiento con el atributo de conexión SQL_ATTR_TRACEFILE. Sin embargo, al hacerlo así no cambia los datos para este valor.|  
  
 Por ejemplo, suponga que está habilitado el seguimiento y el archivo de seguimiento es C:\Odbc.log. Los valores bajo la subclave ODBC sería como sigue:  
  
```  
Trace : REG_SZ : 1  
TraceFile : REG_SZ : C:\ODBC.LOG  
  
```

