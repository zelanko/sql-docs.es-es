---
title: Tipos específicos del conductor - Datos, Descriptor, Información, Diagnóstico ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver-specific diagnostic values [ODBC]
- diagnostic information [ODBC], driver-specific values
- ODBC drivers [ODBC], driver-specific diagnostic values
ms.assetid: ad4c76d3-5191-4262-b47c-5dd1d19d1154
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19bb2dd113fbeae871892ea510713c638c886e5a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305776"
---
# <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>Tipos de datos específicos del controlador, Descriptor tipos, tipos de información, tipos de diagnóstico y atributos
Los controladores pueden asignar valores específicos del controlador para lo siguiente:  
  
-   **Indicadores** de tipo de datos SQL Se utilizan en *ParameterType* en **SQLBindParameter** y en *DataType* en **SQLGetTypeInfo** y devueltos por **SQLColAttribute**, **SQLColumns**, **SQLDescribeCol**, **SQLGetTypeInfo**, **SQLDescribeParam**, **SQLProcedureColumns**y **SQLSpecialColumns**.  
  
-   **Campos descriptores** Se utilizan en *FieldIdentifier* en **SQLColAttribute**, **SQLGetDescField**y **SQLSetDescField**.  
  
-   **Campos de diagnóstico** Se utilizan en *DiagIdentifier* en **SQLGetDiagField** y **SQLGetDiagRec**.  
  
-   **Tipos de información** Se utilizan en *InfoType* en **SQLGetInfo**.  
  
-   **Atributos de conexión e instrucción** Se utilizan en *Atributo* en **SQLGetConnectAttr**, **SQLGetStmtAttr**, **SQLSetConnectAttr**y **SQLSetStmtAttr**.  
  
 Para cada uno de estos elementos, hay dos conjuntos de valores: valores reservados para su uso por ODBC y valores reservados para su uso por los controladores. Antes de implementar valores específicos del controlador, un escritor de controladores debe solicitar un valor para cada tipo, campo o atributo específico del controlador de Open Group. Para el desarrollo de nuevos controladores, utilice el intervalo descrito en la tabla siguiente. El Administrador de controladores ODBC 3.8 no generará un error si se utiliza un valor desconocido que no está en el intervalo descrito a continuación. Sin embargo, las versiones posteriores del Administrador de controladores pueden generar un error si se reciben valores desconocidos que no están en el intervalo.  
  
 Cuando cualquiera de estos valores se pasa a una función ODBC, el controlador debe comprobar si el valor es válido. Los controladores devuelven SQLSTATE HYC00 (característica opcional no implementada) para los valores específicos del controlador que se aplican a otros controladores.  
  
 A partir de ODBC 3.8, los escritores de controladores pueden asignar atributos específicos del controlador dentro de un intervalo reservado.  
  
> [!NOTE]  
>  El Administrador de controladores ODBC 3.8 no valida ni aplica estos intervalos para la compatibilidad con versiones anteriores. Sin embargo, una versión futura del Administrador de controladores podría aplicarlos.  
  
|Tipo de atributo|Tipo de datos de ODBC|Base de rango específica del conductor|Límite de rango específico del conductor|Constante ODBC para la base de rango de valores específica del controlador|  
|--------------------|--------------------|---------------------------------|----------------------------------|---------------------------------------------------------|  
|Indicadores de tipo de datos SQL|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_SQL_TYPE_BASE|  
|Campos descriptores|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DESCRIPTOR_BASE|  
|Campos de diagnóstico|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DIAGNOSTIC_BASE|  
|Tipos de información|SQLUSMALLINT|0x4000|0x7FFF|SQL_DRIVER_INFO_TYPE_BASE|  
|Atributos de conexión|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_CONNECT_ATTR_BASE|  
|Atributos de declaración|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_STATEMENT_ATTR_BASE|  
  
> [!NOTE]  
>  Los tipos de datos específicos del controlador, los campos descriptores, los campos de diagnóstico, los tipos de información, los atributos de instrucción y los atributos de conexión deben describirse en la documentación del controlador. Cuando cualquiera de estos valores se pasa a una función ODBC, el controlador debe comprobar si el valor es válido. Los controladores devuelven SQLSTATE HYC00 (característica opcional no implementada) para los valores específicos del controlador que se aplican a otros controladores.  
  
 Los valores base se definen para facilitar el desarrollo del controlador. Por ejemplo, los atributos de diagnóstico específicos del controlador se pueden definir en el siguiente formato:  
  
```  
SQL_DRIVER_DIAGNOSTIC_BASE+0, SQL_DRIVER_DIAGNOSTIC_BASE +1  
```
