---
title: Tipo de datos de uso | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-results
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
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
caps.latest.revision: "34"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f0e5f5dcda52290332488fc1593f96067b26838e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="data-type-usage"></a>Uso de tipos de datos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] imponen el siguiente uso de tipos de datos.  
  
|Tipo de datos|Limitación|  
|---------------|----------------|  
|Literales de fecha|Literales de fecha, cuando se almacenan en una columna SQL_TYPE_TIMESTAMP ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos de **datetime** o **smalldatetime**), tienen un valor de tiempo de 12:00:00.000 a. M.|  
|**Money** y **smallmoney**|Solo las partes enteras de la **dinero** y **smallmoney** tipos de datos son significativos. Si la parte decimal de SQL **dinero** los datos se truncan durante la conversión de tipo de datos, la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client devuelve una advertencia, no un error.|  
|SQL_BINARY (admite valores NULL)|Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versión 6.0 y anteriores, si una columna SQL_BINARY admite valores NULL, los datos que se almacenan en el origen de datos no se rellenan con ceros. Cuando se recuperan datos de este tipo de columna, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client los rellena con ceros a la derecha. Sin embargo, en los datos que se crean en operaciones realizadas por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como la concatenación, no se realiza este relleno.<br /><br /> Además, cuando los datos se colocan en este tipo de columna en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 o versiones anteriores, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trunca los datos a la derecha si son demasiado largos para ajustarse a la columna.<br /><br /> Nota: La [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client admite la conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 y versiones anteriores.|  
|SQL_CHAR (truncamiento)|Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 y versiones anteriores, si los datos se colocan en una columna SQL_CHAR y son demasiado largos para ajustarse en la columna, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los trunca a la derecha sin ninguna advertencia.<br /><br /> Nota: La [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client admite la conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 y versiones anteriores.|  
|SQL_CHAR (admite valores NULL)|Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 y versiones anteriores, si una columna SQL_CHAR admite valores NULL, los datos almacenados en el origen de datos no se rellenan con espacios en blanco. Cuando se recuperan datos de este tipo de columna, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client rellena con espacios en blanco a la derecha. Sin embargo, en los datos que se crean en operaciones realizadas por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como la concatenación, no se realiza este relleno.<br /><br /> Nota: La [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client admite la conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 y versiones anteriores.|  
|SQL_LONGVARBINARY, SQL_LONGVARCHAR, SQL_WLONGVARCHAR|Las actualizaciones de columnas con SQL_LONGVARBINARY, SQL_LONGVARCHAR o SQL_WLONGVARCHAR tipos de datos (utilizando una cláusula WHERE) que afectan a varias filas son totalmente compatibles cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6. *x* y versiones posteriores. Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 4.2*x*, un error S1000, "inserción/actualización parcial. No se realizó correctamente la inserción o actualización de columnas de texto o de imagen" si la actualización afecta a más de una fila.<br /><br /> Nota: La [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client admite la conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 y versiones anteriores.|  
|Parámetros de función de cadena|*string_exp* parámetros a la cadena de funciones deben ser de tipo SQL_CHAR o SQL_VARCHAR. Los tipos de datos SQL_LONG_VARCHAR no se admiten en las funciones de cadena. El *recuento* parámetro debe ser menor o igual que 8.000 porque los tipos de datos SQL_VARCHAR y SQL_CHAR están limitados a una longitud máxima de 8.000 caracteres.|  
|Literales de hora|Literales de hora, cuando se almacenan en una columna SQL_TIMESTAMP ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos de **datetime** o **smalldatetime**), tiene un valor de fecha del 1 de enero de 1900.|  
|**timestamp**|Solo un valor NULL se puede insertar manualmente en un **timestamp** columna. Sin embargo, dado que **timestamp**columnas se actualizan automáticamente por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se sobrescribe un valor NULL.|  
|**tinyint**|El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **tinyint** tipo de datos es sin signo. A **tinyint** columna se enlaza a una variable de tipo de datos SQL_C_UTINYINT de forma predeterminada.|  
|Tipos de datos de alias|Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 4.2*x*, el controlador ODBC agrega NULL a una definición de columna que no declara explícitamente la nulabilidad de una columna. Por tanto, la nulabilidad almacenada en la definición de un tipo de datos de alias se pasa por alto.<br /><br /> Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 4.2*x*, tipo de columnas con un tipo de datos de alias que tenga una base de datos de **char** o **binario** y para los que no aceptan valores null declara se crean como tipo de datos **varchar** o **varbinary**. [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md), [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md), y [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) devuelven SQL_VARCHAR o SQL_VARBINARY como datos de tipo para estas columnas. Los datos que se recuperan de estas columnas no se rellenan.<br /><br /> Nota: La [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client admite la conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 y versiones anteriores.|  
|Tipos de datos LONG|*datos en ejecución* parámetros están restringidos para SQL_LONGVARBINARY y los tipos de datos SQL_LONGVARCHAR.|  
|Tipos de valores grandes|El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client expondrá **varchar (max)**, **varbinary (max)**, y **nvarchar (max)** tipos como SQL_VARCHAR, SQL_VARBINARY y SQL_ WVARCHAR (respectivamente) en las API que aceptan o devuelven tipos de datos de SQL de ODBC.|  
|Tipo definido por el usuario (UDT)|Las columnas UDT se asignan como SQL_SS_UDT. Si una columna UDT se asigna explícitamente a otro tipo en la instrucción SQL utilizando los métodos ToXMLString () o ToString () del UDT o a través de funciones CAST/CONVERT, el tipo de la columna en el conjunto de resultados reflejará el tipo real en el que se convirtió la columna.<br /><br /> El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client solamente puede enlazar a una columna UDT como binario. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solamente admite la conversión entre los tipos de datos SQL_C_BINARY y SQL_SS_UDT.|  
|XML|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] convertirán automáticamente XML a texto Unicode. El tipo XML se asigna como SQL_SS_XML.|  
  
## <a name="see-also"></a>Vea también  
 [Procesar resultados &#40; ODBC &#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
