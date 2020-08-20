---
description: Subclave ODBC
title: Subclave ODBC | Microsoft Docs
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
ms.openlocfilehash: 4ec27b40e196f5277307b9a299dd865a1604dc0e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499730"
---
# <a name="odbc-subkey"></a>Subclave ODBC
Los valores de la subclave ODBC especifican las opciones de seguimiento de ODBC. Estas opciones se establecen a través de la pestaña seguimiento del cuadro de diálogo Administrador de orígenes de datos ODBC que se muestra en **SQLManageDataSources**. La propia subclave de ODBC es opcional. El formato de estos valores es como se muestra en la tabla siguiente.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|Seguimiento|REG_SZ|**0** &#124; **1**|  
|TraceFile|REG_SZ|*Ruta de acceso de un directorio*|  
  
 Los valores tienen los significados que se describen en la tabla siguiente.  
  
|Value|Significado|  
|-----------|-------------|  
|Seguimiento|Si el valor de seguimiento se establece en 1 cuando una aplicación llama a **SQLAllocHandle** con la opción SQL_HANDLE_ENV, se habilita el seguimiento para la aplicación que realiza la llamada.<br /><br /> Si la palabra clave Trace se establece en 0 cuando una aplicación llama a **SQLAllocHandle** con la opción SQL_HANDLE_ENV, el seguimiento está deshabilitado para la aplicación que realiza la llamada. Este es el valor predeterminado.<br /><br /> Una aplicación puede habilitar o deshabilitar el seguimiento con el atributo de conexión SQL_ATTR_TRACE. Sin embargo, esto no cambia los datos para este valor.|  
|TraceFile|Si el seguimiento está habilitado, el administrador de controladores escribe en el archivo de seguimiento especificado por el valor de seguimiento.<br /><br /> Si no se especifica ningún archivo de seguimiento, el administrador de controladores escribe en el archivo SQL. log de la unidad actual. Este es el valor predeterminado.<br /><br /> El seguimiento debe usarse solo para una sola aplicación o cada aplicación debe especificar un archivo de seguimiento diferente. De lo contrario, dos o más aplicaciones intentarán abrir el mismo archivo de seguimiento al mismo tiempo, lo que producirá un error.<br /><br /> Una aplicación puede especificar un nuevo archivo de seguimiento con el SQL_ATTR_TRACEFILE atributo de conexión. Sin embargo, esto no cambia los datos para este valor.|  
  
 Por ejemplo, supongamos que el seguimiento está habilitado y el archivo de seguimiento es C:\Odbc.log. Los valores de la subclave ODBC serían los siguientes:  
  
```  
Trace : REG_SZ : 1  
TraceFile : REG_SZ : C:\ODBC.LOG  
  
```
