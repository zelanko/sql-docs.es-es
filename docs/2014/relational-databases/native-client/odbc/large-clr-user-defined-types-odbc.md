---
title: Tipos definidos por el usuario CLR grandes (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, large user-defined types
- large user-defined types [ODBC]
ms.assetid: ddce337e-bb6e-4a30-b7cc-4969bb1520a9
author: rothja
ms.author: jroth
ms.openlocfilehash: 62acbe2e9acbf6ba39f982ad43de7a55453f7e3c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055838"
---
# <a name="large-clr-user-defined-types-odbc"></a>Tipos CLR grandes definidos por el usuario (ODBC)
  En este tema se describen los cambios realizados en ODBC en SQL Server Native Client para admitir los tipos definidos por el usuario (UDT) de Common Language Runtime (CLR) grandes.  
  
 Para ver un ejemplo que muestra la compatibilidad de ODBC con los UDT de CLR grandes, consulte [compatibilidad con UDT grandes](../../native-client-odbc-how-to/support-for-large-udts.md).  
  
 Para obtener más información acerca de la compatibilidad con UDT CLR grandes en SQL Server Native Client, consulte [tipos CLR grandes definidos por el usuario](../../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).  
  
## <a name="data-format"></a>Formato de datos  
 SQL Server Native Client usa SQL_SS_LENGTH_UNLIMITED para indicar que el tamaño de una columna es superior a 8.000 bytes para los tipos de objeto grandes (LOB). A partir de SQL Server 2008, se usa el mismo valor para los tipos UDT CLR cuando su tamaño es superior a 8.000 bytes.  
  
 Los valores UDT se representan como matrices de bytes. Se admiten conversiones a cadenas hexadecimales y desde cadenas hexadecimales. Los valores literales se representan como cadenas hexadecimales con el prefijo "0x".  
  
 En la tabla siguiente se muestra la asignación de tipos de datos en parámetros y conjuntos de resultados:  
  
|Tipos de datos de SQL Server|Tipo de datos de SQL|Valor|  
|--------------------------|-------------------|-----------|  
|UDT CLR|SQL_SS_UDT|-151 (sqlncli.h)|  
  
 En la tabla siguiente se describe la estructura y el tipo C de ODBC correspondiente. Esencialmente, un tipo UDT CLR es un tipo `varbinary` con metadatos adicionales.  
  
|Tipo de datos de SQL|Diseño de memoria|Tipo de datos C|Valor (sqlext.h)|  
|-------------------|-------------------|-----------------|------------------------|  
|SQL_SS_UDT|SQLCHAR * (unsigned char \* )|SQL_C_BINARY|SQL_BINARY (-2)|  
  
## <a name="descriptor-fields-for-parameters"></a>Campos descriptores de parámetros  
 La información que se devuelve en los campos IPD es la siguiente:  
  
|Campo descriptor|SQL_SS_UDT<br /><br /> (longitud menor o igual a 8.000 bytes)|SQL_SS_UDT<br /><br /> (longitud mayor que 8.000 bytes)|  
|----------------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CONCISE_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_DATETIME_INTERVAL_CODE|0|0|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_LOCAL_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_OCTET_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_SCALE|0|0|  
|SQL_DESC_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_UNSIGNED|SQL_TRUE|SQL_TRUE|  
|SQL_CA_SS_UDT_CATALOG_NAME|Nombre del catálogo que contiene el UDT.|Nombre del catálogo que contiene el UDT.|  
|SQL_CA_SS_UDT_SCHEMA_NAME|Nombre del esquema que contiene el UDT.|Nombre del esquema que contiene el UDT.|  
|SQL_CA_SS_UDT_TYPE_NAME|Nombre del UDT.|Nombre del UDT.|  
|SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME|Nombre completo del UDT.|Nombre completo del UDT.|  
  
 En el caso de los parámetros UDT, SQL_CA_SS_UDT_TYPE_NAME debe establecerse siempre a través de **SQLSetDescField**. SQL_CA_SS_UDT_CATALOG_NAME y SQL_CA_SS_UDT_SCHEMA_NAME son opcionales.  
  
 Si el UDT se define en la misma base de datos con un esquema distinto que la tabla, debe establecerse SQL_CA_SS_UDT_SCHEMA_NAME.  
  
 Si el UDT se define en una base de datos distinta que la tabla, deben establecerse SQL_CA_SS_UDT_CATALOG_NAME y SQL_CA_SS_UDT_SCHEMA_NAME.  
  
 Si hay algún error u omisión en los valores de SQL_CA_SS_UDT_TYPE_NAME, SQL_CA_SS_UDT_CATALOG_NAME o SQL_CA_SS_UDT_SCHEMA_NAME, se genera un registro de diagnóstico con SQLSTATE HY000 y el texto de mensaje específico del servidor.  
  
## <a name="descriptor-fields-for-results"></a>Campos descriptores de resultados  
 La información que se devuelve en los campos IRD es la siguiente:  
  
|Campo descriptor|SQL_SS_UDT<br /><br /> (longitud menor o igual a 8.000 bytes)|SQL_SS_UDT<br /><br /> (longitud mayor que 8.000 bytes)|  
|----------------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CONCISE_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_DATETIME_INTERVAL_CODE|0|0|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_DISPLAY_SIZE|2*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_LITERAL_PREFIX|"0x"|"0x"|  
|SQL_DESC_LITERAL_SUFFIX|""|""|  
|SQL_DESC_LOCAL_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_OCTET_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_SCALE|0|0|  
|SQL_DESC_SEARCHABLE|SQL_PRED_NONE|SQL_PRED_NONE|  
|SQL_DESC_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_UNSIGNED|SQL_TRUE|SQL_TRUE|  
|SQL_CA_SS_UDT_CATALOG_NAME|Nombre del catálogo que contiene el UDT.|Nombre del catálogo que contiene el UDT.|  
|SQL_CA_SS_UDT_SCHEMA_NAME|Nombre del esquema que contiene el UDT.|Nombre del esquema que contiene el UDT.|  
|SQL_CA_SS_UDT_TYPE_NAME|Nombre del UDT.|Nombre del UDT.|  
|SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME|Nombre completo del UDT.|Nombre completo del UDT.|  
  
## <a name="column-metadata-returned-by-sqlcolumns-and-sqlprocedurecolumns-catalog-metadata"></a>Metadatos de columna devueltos por SQLColumns y SQLProcedureColumns (metadatos de catálogo)  
 Para los UDT se devuelven los siguientes valores de columna:  
  
|Nombre de la columna|SQL_SS_UDT<br /><br /> (longitud menor o igual a 8.000 bytes)|SQL_SS_UDT<br /><br /> (longitud mayor que 8.000 bytes)|  
|-----------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|DATA_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|TYPE_NAME|Nombre del UDT.|Nombre del UDT.|  
|COLUMN_SIZE|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|BUFFER_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|DECIMAL_DIGITS|NULL|NULL|  
|SQL_DATA_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DATETIME_SUB|NULL|NULL|  
|CHAR_OCTET_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SS_UDT_CATALOG_NAME|Nombre del catálogo que contiene el UDT.|Nombre del catálogo que contiene el UDT.|  
|SS_UDT_SCHEMA_NAME|Nombre del esquema que contiene el UDT.|Nombre del esquema que contiene el UDT.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|Nombre completo del UDT.|Nombre completo del UDT.|  
  
 Las últimas tres columnas son columnas específicas del controlador. Se agregan después de cualquier columna definida por ODBC, pero antes de cualquier columna específica del controlador existente del conjunto de resultados de SQLColumns o SQLProcedureColumns.  
  
 SQLGetTypeInfo no devuelve ninguna fila, para los UDT individuales o para el tipo genérico "UDT".  
  
## <a name="bindings-and-conversions"></a>Enlaces y conversiones  
 Las conversiones compatibles de tipos de datos SQL a C son las siguientes:  
  
|Conversión a y desde:|SQL_SS_UDT|  
|-----------------------------|------------------|  
|SQL_C_WCHAR|Realizar|  
|SQL_C_BINARY|Compatible|  
|SQL_C_CHAR|Realizar|  
  
 \*Los datos binarios se convierten en una cadena hexadecimal.  
  
 Las conversiones compatibles de tipos de datos C a SQL son las siguientes:  
  
|Conversión a y desde:|SQL_SS_UDT|  
|-----------------------------|------------------|  
|SQL_C_WCHAR|Realizar|  
|SQL_C_BINARY|Compatible|  
|SQL_C_CHAR|Realizar|  
  
 \*Se produce una conversión de cadena hexadecimal a datos binarios.  
  
## <a name="sql_variant-support-for-udts"></a>Compatibilidad de SQL_VARIANT con los UDT  
 Los UDT no se admiten en columnas SQL_VARIANT.  
  
## <a name="bcp-support-for-udts"></a>Compatibilidad de BCP con los UDT  
 Los valores UDT pueden importarse y exportarse solo como valores de caracteres o binarios.  
  
## <a name="downlevel-client-behavior-for-udts"></a>Comportamiento del cliente de nivel inferior en los UDT  
 Los UDT están sujetos a la asignación de tipos con clientes de nivel inferior, tal y como se indica a continuación:  
  
|Versión del servidor|SQL_SS_UDT<br /><br /> (longitud menor o igual a 8.000 bytes)|SQL_SS_UDT<br /><br /> (longitud mayor que 8.000 bytes)|  
|--------------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|SQL Server 2005|`UDT`|`varbinary(max)`|  
|SQL Server 2008 y posterior|`UDT`|`UDT`|  
  
## <a name="odbc-functions-supporting-large-clr-udts"></a>Funciones ODBC compatibles con UDT de CLR grandes  
 En esta sección se describen los cambios realizados en las funciones ODBC de SQL Server Native Client para admitir UDT de CLR grandes.  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 Los valores de las columnas de resultados UDT se convierten de tipos de los tipos de usuario de SQL a C, como se describe en la sección "enlaces y conversiones", anteriormente en este tema.  
  
### <a name="sqlbindparameter"></a>SQLBindParameter  
 Los valores requeridos para los UDT son los siguientes:  
  
|Tipo de datos de SQL|*Parametertype*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-------------------|---------------------|---------------------|------------------------|  
|SQL_SS_UDT<br /><br /> (longitud menor o igual a 8.000 bytes)|SQL_SS_UDT|*n*|0|  
|SQL_SS_UDT<br /><br /> (longitud mayor que 8.000 bytes)|SQL_SS_UDT|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 Los valores devueltos para los UDT son los que se describían en la sección "Campos descriptores de resultados" anteriormente en este tema.  
  
### <a name="sqlcolumns"></a>SQLColumns  
 Los valores devueltos para los UDT son los que se describen en la sección "metadatos de columna devueltos por SQLColumns y SQLProcedureColumns (metadatos de catálogo)", anteriormente en este tema.  
  
### <a name="sqldescribecol"></a>SQLDescribeCol  
 Los valores devueltos para los UDT son los siguientes:  
  
|Tipo de datos de SQL|*DataTypePtr*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-------------------|-------------------|---------------------|------------------------|  
|SQL_SS_UDT<br /><br /> (longitud menor o igual a 8.000 bytes)|SQL_SS_UDT|*n*|0|  
|SQL_SS_UDT<br /><br /> (longitud mayor que 8.000 bytes)|SQL_SS_UDT|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqldescribeparam"></a>SQLDescribeParam  
 Los valores devueltos para los UDT son los siguientes:  
  
|Tipo de datos de SQL|*DataTypePtr*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-------------------|-------------------|---------------------|------------------------|  
|SQL_SS_UDT<br /><br /> (longitud menor o igual a 8.000 bytes)|SQL_SS_UDT|*n*|0|  
|SQL_SS_UDT<br /><br /> (longitud mayor que 8.000 bytes)|SQL_SS_UDT|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlfetch"></a>SQLFetch  
 Los valores de las columnas de resultados UDT se convierten de tipos de los tipos de usuario de SQL a C, como se describe en la sección "enlaces y conversiones", anteriormente en este tema.  
  
### <a name="sqlfetchscroll"></a>SQLFetchScroll  
 Los valores de las columnas de resultados UDT se convierten de tipos de los tipos de usuario de SQL a C, como se describe en la sección "enlaces y conversiones", anteriormente en este tema.  
  
### <a name="sqlgetdata"></a>SQLGetData  
 Los valores de las columnas de resultados UDT se convierten de tipos de los tipos de usuario de SQL a C, como se describe en la sección "enlaces y conversiones", anteriormente en este tema.  
  
### <a name="sqlgetdescfield"></a>SQLGetDescField  
 Los campos descriptores disponibles con los nuevos tipos se describen en las secciones "Campos descriptores de parámetros" y "Campos descriptores de resultados" anteriormente en este tema.  
  
### <a name="sqlgetdescrec"></a>SQLGetDescRec  
 Los valores devueltos para los UDT son los siguientes:  
  
|Tipo de datos de SQL|Tipo|SubType|Length|Precisión|Escala|  
|-------------------|----------|-------------|------------|---------------|-----------|  
|SQL_SS_UDT<br /><br /> (longitud menor o igual a 8.000 bytes)|SQL_SS_UDT|0|*n*|n|0|  
|SQL_SS_UDT<br /><br /> (longitud mayor que 8.000 bytes)|SQL_SS_UDT|0|SQL_SS_LENGTH_UNLIMITED (0)|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlgettypeinfo"></a>SQLGetTypeInfo  
 Los valores devueltos para los UDT son los que se describían en la sección "Metadatos de columna devueltos por SQLColumns y SQLProcedureColumns (metadatos de catálogo)" anteriormente en este tema.  
  
### <a name="sqlprocedurecolumns"></a>SQLProcedureColumns  
 Los valores devueltos para los UDT son los que se describían en la sección "Metadatos de columna devueltos por SQLColumns y SQLProcedureColumns (metadatos de catálogo)" anteriormente en este tema.  
  
### <a name="sqlputdata"></a>SQLPutData  
 Los valores de los parámetros UDT se convierten de C a tipos de SQL como se describe en la sección "enlaces y conversiones", anteriormente en este tema.  
  
### <a name="sqlsetdescfield"></a>SQLSetDescField  
 El campo descriptor disponible con los nuevos tipos se describe en las secciones "Campos descriptores de parámetros" y "Campos descriptores de resultados" anteriormente en este tema.  
  
### <a name="sqlsetdescrec"></a>SQLSetDescRec  
 Los valores que se permiten para los UDT son los siguientes:  
  
|Tipo de datos de SQL|Tipo|SubType|Length|Precisión|Escala|  
|-------------------|----------|-------------|------------|---------------|-----------|  
|SQL_SS_UDT<br /><br /> (longitud menor o igual a 8.000 bytes)|SQL_SS_UDT|0|*n*|*n*|0|  
|SQL_SS_UDT<br /><br /> (longitud mayor que 8.000 bytes)|SQL_SS_UDT|0|SQL_SS_LENGTH_UNLIMITED (0)|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlspecialcolumns"></a>SQLSpecialColumns  
 Los valores devueltos para las columnas de los UDT DATA_TYPE, TYPE_NAME, COLUMN_SIZE, BUFFER_LENGTH y UDT DECIMAL_DIGTS son los que se describían en la sección "Metadatos devueltos por SQLColumns y SQLProcedureColumns (metadatos de catálogo)" anteriormente en este tema.  
  
## <a name="see-also"></a>Consulte también  
 [Tipos definidos por el usuario de CLR grandes](../../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
