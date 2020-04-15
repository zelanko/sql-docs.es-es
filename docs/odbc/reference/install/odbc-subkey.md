---
title: Subclave ODBC (ODBC Subkey) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96e9a5f4c3cdac5097686528d3c089d9ec5826f7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287445"
---
# <a name="odbc-subkey"></a>Subclave ODBC
Los valores de la subclave ODBC especifican opciones de seguimiento ODBC. Estas opciones se establecen a través de la pestaña Seguimiento del cuadro de diálogo Administrador de orígenes de datos ODBC que muestra **SQLManageDataSources**. La subclave ODBC en sí es opcional. El formato de estos valores es como se muestra en la tabla siguiente.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|Seguimiento|REG_SZ|**0** &#124; **1**|  
|TraceFile|REG_SZ|*tracefile-path*|  
  
 Los valores tienen los significados descritos en la tabla siguiente.  
  
|Value|Significado|  
|-----------|-------------|  
|Seguimiento|Si el valor de seguimiento se establece en 1 cuando una aplicación llama a **SQLAllocHandle** con la opción SQL_HANDLE_ENV, el seguimiento está habilitado para la aplicación que realiza la llamada.<br /><br /> Si la palabra clave Trace se establece en 0 cuando una aplicación llama a **SQLAllocHandle** con la opción SQL_HANDLE_ENV, el seguimiento está deshabilitado para la aplicación que realiza la llamada. Este es el valor predeterminado.<br /><br /> Una aplicación puede habilitar o deshabilitar el seguimiento con el atributo de conexión SQL_ATTR_TRACE. Sin embargo, al hacerlo no se cambian los datos de este valor.|  
|TraceFile|Si el seguimiento está habilitado, el Administrador de controladores escribe en el archivo de seguimiento especificado por el TraceFile valor.<br /><br /> Si no se especifica ningún archivo de seguimiento, el Administrador de controladores escribe en el archivo Sql.log de la unidad actual. Este es el valor predeterminado.<br /><br /> El seguimiento solo se debe usar para una sola aplicación o cada aplicación debe especificar un archivo de seguimiento diferente. De lo contrario, dos o más aplicaciones intentarán abrir el mismo archivo de seguimiento al mismo tiempo, lo que provocará un error.<br /><br /> Una aplicación puede especificar un nuevo archivo de seguimiento con el atributo de conexión SQL_ATTR_TRACEFILE. Sin embargo, al hacerlo no se cambian los datos de este valor.|  
  
 Por ejemplo, supongamos que el seguimiento está habilitado y el archivo de seguimiento es C:-Odbc.log. Los valores de la subclave ODBC serían los siguientes:  
  
```  
Trace : REG_SZ : 1  
TraceFile : REG_SZ : C:\ODBC.LOG  
  
```
