---
title: Campos de descriptor de parámetros con valores de tabla | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), descriptor fields
ms.assetid: 4e009eff-c156-4d63-abcf-082ddd304de2
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f97d723d027cb756e7a74b5f2aa58c06d0d63acd
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760658"
---
# <a name="table-valued-parameter-descriptor-fields"></a>Campos de descriptor de parámetros con valores de tabla
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  La compatibilidad con los parámetros con valores de tabla incluye nuevos campos específicos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en descriptores de parámetros de aplicación ODBC (APD) y descriptores de parámetros de implementación (IPD).  
  
## <a name="remarks"></a>Comentarios  
  
|Nombre|Location|Tipo|Descripción|  
|----------|--------------|----------|-----------------|  
|SQL_CA_SS_TYPE_NAME|IPD|SQLTCHAR*|Nombre del tipo de servidor del parámetro con valores de tabla.<br /><br /> Cuando se especifica un nombre de tipo de parámetro con valores de tabla en una llamada a SQLBindParameter, siempre debe especificarse como un valor Unicode, incluso en aplicaciones compiladas como aplicaciones ANSI. El valor usado para el parámetro *StrLen_or_IndPtr* debe ser SQL_NTS o la longitud de la cadena del nombre multiplicado por SIZEOF (WCHAR).<br /><br /> Cuando se especifica un nombre de tipo de parámetro con valores de tabla a través de SQLSetDescField, se puede especificar mediante un literal que se ajuste a la manera en que se compila la aplicación. El administrador de controladores ODBC realizará cualquier conversión Unicode que sea necesaria.|  
|SQL_CA_SS_TYPE_CATALOG_NAME (solo lectura)|IPD|SQLTCHAR*|Catálogo donde se define el tipo.|  
|SQL_CA_SS_TYPE_SCHEMA_NAME|IPD|SQLTCHAR*|Esquema donde se define el tipo.|  
  
 Las aplicaciones no deben establecer SQL_CA_SS_TYPE_CATALOG_NAME en parámetros con valores de tabla. Si se establece, se devolverá SQL_ERROR y se registrará un error de diagnóstico con SQLSTATE = HY091 y el mensaje "identificador de campo descriptor no válido".  
  
 Cuando el enfoque del parámetro se establece en un parámetro con valores de tabla, se aplican los siguientes campos de encabezado de descriptor y atributos de instrucción a los parámetros con valores de tabla:  
  
|Nombre|Location|Tipo|Descripción|  
|----------|--------------|----------|-----------------|  
|SQL_ATTR_PARAMSET_SIZE<br /><br /> (Equivalente a SQL_DESC_ARRAY_SIZE en el APD.)|APD|SQLUINTEGER|Tamaño de matriz de las matrices de búfer de un parámetro con valores de tabla. Éste es el número máximo de filas que los búferes pueden incluir o el tamaño de los búferes en filas; el propio valor de parámetro con valores de tabla puede tener más o menos filas de las que pueden incluir los búferes. El valor predeterminado es 1.<br /><br /> Nota: si SQL_SOPT_SS_PARAM_FOCUS se establece en su valor predeterminado de 0, SQL_ATTR_PARAMSET_SIZE hace referencia a la instrucción y especifica el número de conjuntos de parámetros. Si SQL_SOPT_SS_PARAM_FOCUS se establece en el ordinal de un parámetro con valores de tabla, hace referencia al parámetro con valores de tabla y especifica el número de filas por conjunto de parámetros del parámetro con valores de tabla.|  
|SQL_ATTR_PARAM _BIND_TYPE|APD|SQLINTEGER|El valor predeterminado es SQL_PARAM_BIND_BY_COLUMN.<br /><br /> Para seleccionar el enlace de modo de fila, este campo se establece en la longitud de la estructura o en una instancia de un búfer que se enlazará a un conjunto de filas de parámetro con valores de tabla. Esta longitud debe incluir el espacio para todas las columnas enlazadas y cualquier relleno de la estructura o búfer. De esta forma se garantiza que, cuando la dirección de una columna enlazada se incrementa con la longitud especificada, el resultado señalará al principio de la misma columna en la fila siguiente. Al usar el operador **sizeof** en ANSI C, se garantiza este comportamiento.|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|APD|SQLINTEGER*|El valor predeterminado es un puntero NULL.<br /><br /> Si este campo es no NULL, el controlador elimina las referencias el puntero, agrega el valor sin referencia a cada uno de los campos aplazados del registro de descriptor (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR y SQL_DESC_OCTET_LENGTH_PTR) y utiliza los nuevos valores de puntero para tener acceso a los valores de datos.|  
  
 Estos campos solo son válidos con parámetros con valores de tabla y se omiten en otros tipos de datos.  
  
 SQL_CA_SS_TYPE_NAME es opcional para las llamadas a procedimientos almacenados. Se debe especificar en instrucciones SQL que no son llamadas a procedimientos para permitir que el servidor determine el tipo de parámetro con valores de tabla.  
  
 Si se necesita el nombre de tipo y el tipo de tabla del parámetro con valores de tabla se define en un esquema diferente del procedimiento almacenado, se debe especificar SQL_CA_SS_TYPE_SCHEMA_NAME en el descriptor del parámetro de implementación (IPD). Si no se especifica, el servidor no podrá determinar el tipo del parámetro con valores de tabla. Esto producirá un error al llamar a SQLExecute o SQLExecDirect. El error tendrá SQLSTATE = 07006 y el mensaje "Infracción del atributo de tipo de datos restringido".  
  
 Las columnas de parámetros con valores de tabla pueden utilizar el enlace de modo de fila o de modo de columna. El valor predeterminado es el enlace de modo de columna. El enlace de modo de fila se puede especificar estableciendo SQL_ATTR_PARAM_BIND_TYPE y SQL_ATTR_ PARAM_BIND_OFFSET_PTR. Es similar al enlace de modo de fila de columnas y parámetros.  
  
 SQL_CA_SS_TYPE_CATALOG_NAME y SQL_CA_SS_TYPE_SCHEMA_NAME también pueden utilizarse para recuperar el catálogo y el esquema asociados a parámetros de tipo definidos por el usuario CLR. Éstas son las alternativas a los atributos de esquema y catálogo específicos del tipo existentes para estos tipos.  
  
## <a name="see-also"></a>Consulte también  
 [Parámetros con valores de tabla &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
