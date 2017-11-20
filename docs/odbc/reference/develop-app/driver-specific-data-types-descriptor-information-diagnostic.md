---
title: "Diagnóstico de Descriptor de acceso, información, de tipos específicos del controlador: datos, | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- driver-specific diagnostic values [ODBC]
- diagnostic information [ODBC], driver-specific values
- ODBC drivers [ODBC], driver-specific diagnostic values
ms.assetid: ad4c76d3-5191-4262-b47c-5dd1d19d1154
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 05aaeca12342ec9d037595ff001a0d1edc745818
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>Tipos de datos específicos del controlador, Descriptor tipos, tipos de información, tipos de diagnóstico y atributos
Controladores pueden asignar valores específicos del controlador para lo siguiente:  
  
-   **Indicadores de tipo de datos de SQL** se utilizan en *ParameterType* en **SQLBindParameter** y en *DataType* en **SQLGetTypeInfo** y devolviendo **SQLColAttribute**, **SQLColumns**, **SQLDescribeCol**, **SQLGetTypeInfo**,  **SQLDescribeParam**, **SQLProcedureColumns**, y **SQLSpecialColumns**.  
  
-   **Campos de descriptor** se utilizan en *FieldIdentifier* en **SQLColAttribute**, **SQLGetDescField**, y **SQLSetDescField** .  
  
-   **Campos de diagnóstico** se utilizan en *DiagIdentifier* en **SQLGetDiagField** y **SQLGetDiagRec**.  
  
-   **Tipos de información** se utilizan en *tipo de información* en **SQLGetInfo**.  
  
-   **Conexión y los atributos de instrucción** se utilizan en *atributo* en **SQLGetConnectAttr**, **SQLGetStmtAttr**,  **SQLSetConnectAttr**, y **SQLSetStmtAttr**.  
  
 Para cada uno de estos elementos, hay dos conjuntos de valores: valores reservados para su uso por ODBC y los valores reservados para su uso por los controladores. Antes de implementar los valores específicos del controlador, un escritor de controlador debe solicitar un valor para cada tipo específico del controlador, campo o atributo de Open Group. Para nuevas implementaciones de controlador, utilice el intervalo que se describe en la tabla siguiente. El Administrador de ODBC 3.8 controladores no generará un error si se utiliza un valor desconocido que no está en el intervalo que se describe a continuación. Sin embargo, las versiones posteriores del Administrador de controladores podrían generarse un error si no se reciben que no están en el intervalo de valores desconocidos.  
  
 Cuando ninguno de estos valores se pasan a una función ODBC, el controlador debe comprobar si el valor es válido. Controladores devuelven SQLSTATE HYC00 (característica opcional no implementada) para los valores específicos del controlador que se aplican a otros controladores.  
  
 A partir de ODBC 3.8, escritores de controlador pueden asignar atributos específicos del controlador dentro de un intervalo reservado.  
  
> [!NOTE]  
>  El Administrador de ODBC 3.8 controladores no valida ni aplica estos intervalos para la compatibilidad con versiones anteriores. Una versión futura del Administrador de controladores puede aplicarlas, sin embargo.  
  
|Tipo de atributo|Tipo de datos de ODBC|Intervalo específicos del controlador base|Límite de intervalo específicos del controlador|Constante ODBC para el intervalo de valores específicos del controlador de base|  
|--------------------|--------------------|---------------------------------|----------------------------------|---------------------------------------------------------|  
|Indicadores de tipo de datos SQL|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_SQL_TYPE_BASE|  
|Campos de descriptor|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DESCRIPTOR_BASE|  
|Campos de diagnóstico|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DIAGNOSTIC_BASE|  
|Tipos de información|SQLUSMALLINT|0x4000|0x7FFF|SQL_DRIVER_INFO_TYPE_BASE|  
|Atributos de conexión|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_CONNECT_ATTR_BASE|  
|Atributos de instrucción|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_STATEMENT_ATTR_BASE|  
  
> [!NOTE]  
>  Tipos de datos específicos del controlador, campos de descriptor, campos de diagnóstico, tipos de información, los atributos de instrucción y atributos de conexión deben describir en la documentación del controlador. Cuando ninguno de estos valores se pasan a una función ODBC, el controlador debe comprobar si el valor es válido. Controladores devuelven SQLSTATE HYC00 (característica opcional no implementada) para los valores específicos del controlador que se aplican a otros controladores.  
  
 Los valores base se definen para facilitar el desarrollo del controlador. Por ejemplo, se pueden definir atributos de diagnóstico específicos del controlador en el formato siguiente:  
  
```  
SQL_DRIVER_DIAGNOSTIC_BASE+0, SQL_DRIVER_DIAGNOSTIC_BASE +1  
```

