---
title: Subclave de ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- registry entries for data sources [ODBC], ODBC subkey
- subkeys [ODBC], ODBC subkey
- ODBC subkey [ODBC]
ms.assetid: f9534144-8f42-4946-b0fb-638e9dcde9c8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ee7cf624e7c118a5d9ef36738c810aecc4ec5684
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63281008"
---
# <a name="odbc-subkey"></a>Subclave ODBC
Los valores bajo la subclave ODBC especifican las opciones de seguimiento de ODBC. Estas opciones se establecen a través de la ficha trazas del cuadro de diálogo Administrador de orígenes de datos ODBC muestra **SQLManageDataSources**. La propia subclave ODBC es opcional. El formato de estos valores es como se muestra en la tabla siguiente.  
  
|Name|Tipo de datos|Datos|  
|----------|---------------|----------|  
|Trace|REG_SZ|**0** &#124; **1**|  
|TraceFile|REG_SZ|*tracefile-path*|  
  
 Los valores tienen los significados que se describen en la tabla siguiente.  
  
|Valor|Significado|  
|-----------|-------------|  
|Trace|Si el valor de seguimiento está establecido en 1 cuando una aplicación llama a **SQLAllocHandle** con la opción de SQL_HANDLE_ENV, el seguimiento está habilitado para la aplicación que realiza la llamada.<br /><br /> Si la palabra clave de seguimiento se establece en 0 cuando una aplicación llama a **SQLAllocHandle** con la opción de SQL_HANDLE_ENV seguimiento está deshabilitado para la aplicación que realiza la llamada. Este es el valor predeterminado.<br /><br /> Una aplicación puede habilitar o deshabilitar el seguimiento con el atributo de conexión SQL_ATTR_TRACE. Sin embargo, si lo hace por lo que no cambia los datos para este valor.|  
|TraceFile|Si está habilitada la traza, el Administrador de controladores se escribe en el archivo de seguimiento especificado por el valor del archivo de seguimiento.<br /><br /> Si se especifica ningún archivo de seguimiento, el Administrador de controladores se escribe en el archivo Sql.log en la unidad actual. Este es el valor predeterminado.<br /><br /> El seguimiento debe usarse solo para una sola aplicación, o cada aplicación debe especificar un archivo de seguimiento diferente. En caso contrario, dos o más aplicaciones intentará abrir el mismo archivo de seguimiento al mismo tiempo, produciendo un error.<br /><br /> Una aplicación puede especificar un nuevo archivo de seguimiento con el atributo de conexión SQL_ATTR_TRACEFILE. Sin embargo, si lo hace por lo que no cambia los datos para este valor.|  
  
 Por ejemplo, suponga que está habilitada la traza y el archivo de seguimiento es C:\Odbc.log. Los valores bajo la subclave ODBC sería como sigue:  
  
```  
Trace : REG_SZ : 1  
TraceFile : REG_SZ : C:\ODBC.LOG  
  
```
