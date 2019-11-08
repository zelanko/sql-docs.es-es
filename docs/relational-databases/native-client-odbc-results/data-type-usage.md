---
title: Uso del tipo de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC data types
- ODBC data types, about ODBC data types
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- data types [ODBC]
- SQL Server Native Client ODBC driver, data types
- data types [ODBC], about data types
ms.assetid: 4f19b0d6-94ac-4a98-a121-57d38787864c
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c0ec45270c7ecd33dae1a441499adefabcc61bb3
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73779263"
---
# <a name="data-type-usage"></a>Uso de tipos de datos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] imponen el siguiente uso de los tipos de datos.  
  
|Tipo de datos|Limitación|  
|---------------|----------------|  
|Literales de fecha|Los literales de fecha, cuando se almacenan en una SQL_TYPE_TIMESTAMP columna ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos de **DateTime** o **smalldatetime**), tienen un valor de tiempo de 12:00:00.000 A.M.|  
|**Money** y **smallmoney**|Solo las partes enteras de los tipos de datos **Money** y **smallmoney** son significativas. Si la parte decimal de los datos de **Money** de SQL se trunca durante la conversión del tipo de datos, el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client devuelve una advertencia, no un error.|  
|SQL_BINARY (admite valores NULL)|Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versión 6.0 y anteriores, si una columna SQL_BINARY admite valores NULL, los datos que se almacenan en el origen de datos no se rellenan con ceros. Cuando se recuperan los datos de esta columna, el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client lo rellena con ceros a la derecha. Sin embargo, en los datos que se crean en operaciones realizadas por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como la concatenación, no se realiza este relleno.<br /><br /> Además, cuando los datos se colocan en este tipo de columna en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 o versiones anteriores, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trunca los datos a la derecha si son demasiado largos para ajustarse a la columna.<br /><br /> Nota: el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client admite la conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6,5 y versiones anteriores.|  
|SQL_CHAR (truncamiento)|Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 y versiones anteriores, si los datos se colocan en una columna SQL_CHAR y son demasiado largos para ajustarse en la columna, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los trunca a la derecha sin ninguna advertencia.<br /><br /> Nota: el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client admite la conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6,5 y versiones anteriores.|  
|SQL_CHAR (admite valores NULL)|Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 y versiones anteriores, si una columna SQL_CHAR admite valores NULL, los datos almacenados en el origen de datos no se rellenan con espacios en blanco. Cuando se recuperan los datos de esta columna, el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client lo rellena con espacios en blanco a la derecha. Sin embargo, en los datos que se crean en operaciones realizadas por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como la concatenación, no se realiza este relleno.<br /><br /> Nota: el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client admite la conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6,5 y versiones anteriores.|  
|SQL_LONGVARBINARY, SQL_LONGVARCHAR, SQL_WLONGVARCHAR|Las actualizaciones de columnas con SQL_LONGVARBINARY, SQL_LONGVARCHAR o SQL_WLONGVARCHAR tipos de datos (con una cláusula WHERE) que afectan a varias filas son totalmente compatibles cuando se conectan a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6. *x* y versiones posteriores. Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 4,2*x*, un error S1000, "inserción o actualización parcial. No se realizó correctamente la inserción o actualización de columnas de texto o de imagen" si la actualización afecta a más de una fila.<br /><br /> Nota: el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client admite la conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6,5 y versiones anteriores.|  
|Parámetros de función de cadena|*string_exp* parámetros de las funciones de cadena deben ser de tipo de datos SQL_CHAR o SQL_VARCHAR. Los tipos de datos SQL_LONG_VARCHAR no se admiten en las funciones de cadena. El parámetro *Count* debe ser menor o igual que 8.000 porque los tipos de datos SQL_CHAR y SQL_VARCHAR se limitan a una longitud máxima de 8.000 caracteres.|  
|Literales de hora|Los literales de hora, cuando se almacenan en una SQL_TIMESTAMP columna ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos de **DateTime** o **smalldatetime**), tienen un valor de fecha del 1 de enero de 1900.|  
|**timestamp**|Solo se puede insertar manualmente un valor NULL en una columna **timestamp** . Sin embargo, dado que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]actualiza automáticamente las columnas de **marca**de tiempo, se sobrescribe un valor null.|  
|**tinyint**|El tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **tinyint** es sin signo. Una columna **tinyint** se enlaza a una variable de tipo de datos SQL_C_UTINYINT de forma predeterminada.|  
|Tipos de datos de alias|Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 4,2*x*, el controlador ODBC agrega null a una definición de columna que no declara explícitamente la nulabilidad de una columna. Por tanto, la nulabilidad almacenada en la definición de un tipo de datos de alias se pasa por alto.<br /><br /> Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 4,2*x*, las columnas con un tipo de datos de alias que tiene un tipo de datos base **Char** o **Binary** y para las que no se declara ninguna nulabilidad se crean como tipo de datos **VARCHAR** o **varbinary**. [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md), [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)y [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) devuelven SQL_VARCHAR o SQL_VARBINARY como tipo de datos para estas columnas. Los datos que se recuperan de estas columnas no se rellenan.<br /><br /> Nota: el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client admite la conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6,5 y versiones anteriores.|  
|Tipos de datos LONG|los parámetros de *datos en ejecución* están restringidos para los tipos de datos SQL_LONGVARBINARY y SQL_LONGVARCHAR.|  
|Tipos de valores grandes|El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client expondrá los tipos **VARCHAR (Max)** , **varbinary (Max)** y **nvarchar (max)** como SQL_VARCHAR, SQL_VARBINARY y SQL_WVARCHAR (respectivamente) en las API que aceptan o devuelven tipos de datos ODBC SQL.|  
|Tipo definido por el usuario (UDT)|Las columnas UDT se asignan como SQL_SS_UDT. Si una columna UDT se asigna explícitamente a otro tipo en la instrucción SQL utilizando los métodos ToXMLString () o ToString () del UDT o a través de funciones CAST/CONVERT, el tipo de la columna en el conjunto de resultados reflejará el tipo real en el que se convirtió la columna.<br /><br /> El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client solo se puede enlazar a una columna UDT como binario. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solamente admite la conversión entre los tipos de datos SQL_C_BINARY y SQL_SS_UDT.|  
|XML|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] convertirán automáticamente XML a texto Unicode. El tipo XML se asigna como SQL_SS_XML.|  
  
## <a name="see-also"></a>Vea también  
 [Procesar resultados &#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
