---
title: SQLColAttribute | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLColAttribute function
ms.assetid: a5387d9e-a243-4cfe-b786-7fad5842b1d6
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6113316f3be68ca03b5c107ed54965577b6963c8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302638"
---
# <a name="sqlcolattribute"></a>SQLColAttribute
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Puede usar **SQLColAttribute** para recuperar un atributo de una columna de conjunto de resultados para instrucciones ODBC preparadas o ejecutadas. Llamar a **SQLColAttribute** en instrucciones preparadas provoca una acción de ida y vuelta (round trip) a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client recibe los datos de la columna de conjunto de resultados como parte de la ejecución de la instrucción, de modo que la llamada a **SQLColAttribute** tras la ejecución de **SQLExecute** o **SQLExecDirect** no implica ninguna acción de ida y vuelta (round trip) al servidor.  
  
> [!NOTE]  
>  Los atributos de identificador de columna de ODBC no están disponibles en todos los conjuntos de resultados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Identificador de campo|Descripción|  
|----------------------|-----------------|  
|SQL_COLUMN_TABLE_NAME|Disponible en conjuntos de resultados recuperados de instrucciones que generan cursores de servidor o en instrucciones SELECT ejecutadas que contienen una cláusula FOR BROWSE.|  
|SQL_DESC_BASE_COLUMN_NAME|Disponible en conjuntos de resultados recuperados de instrucciones que generan cursores de servidor o en instrucciones SELECT ejecutadas que contienen una cláusula FOR BROWSE.|  
|SQL_DESC_BASE_TABLE_NAME|Disponible en conjuntos de resultados recuperados de instrucciones que generan cursores de servidor o en instrucciones SELECT ejecutadas que contienen una cláusula FOR BROWSE.|  
|SQL_DESC_CATALOG_NAME|nombre de base de datos. Disponible en conjuntos de resultados recuperados de instrucciones que generan cursores de servidor o en instrucciones SELECT ejecutadas que contienen una cláusula FOR BROWSE.|  
|SQL_DESC_LABEL|Disponible en todos los conjuntos de resultados. El valor es idéntico al valor del campo SQL_DESC_NAME.<br /><br /> El campo solo tiene longitud cero si una columna es el resultado de una expresión y la expresión no contiene ninguna asignación de etiqueta.|  
|SQL_DESC_NAME|Disponible en todos los conjuntos de resultados. El valor es idéntico al valor del campo SQL_DESC_LABEL.<br /><br /> El campo solo tiene longitud cero si una columna es el resultado de una expresión y la expresión no contiene ninguna asignación de etiqueta.|  
|SQL_DESC_SCHEMA_NAME|Nombre del propietario. Disponible en conjuntos de resultados recuperados de instrucciones que generan cursores de servidor o en instrucciones SELECT ejecutadas que contienen una cláusula FOR BROWSE.<br /><br /> Solo disponible si se especifica el nombre del propietario de la columna en la instrucción SELECT.|  
|SQL_DESC_TABLE_NAME|Disponible en conjuntos de resultados recuperados de instrucciones que generan cursores de servidor o en instrucciones SELECT ejecutadas que contienen una cláusula FOR BROWSE.|  
|SQL_DESC_UNNAMED|SQL_NAMED en todas las columnas de un conjunto de resultados, a menos que una columna sea el resultado de una expresión que no contiene ninguna asignación de etiqueta como parte de la expresión. Cuando SQL_DESC_UNNAMED devuelve SQL_UNNAMED, todos los atributos de identificador de columna de ODBC contienen cadenas de longitud cero en la columna.|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]El controlador ODBC de Native Client usa la instrucción SET FMTONLY para reducir la sobrecarga del servidor cuando se llama a **SQLColAttribute** para las instrucciones preparadas pero no ejecutadas.  
  
 Para tipos de valor grande, **SQLColAttribute** devolverá los valores siguientes:  
  
|Identificador de campo|Descripción del cambio|  
|----------------------|---------------------------|  
|SQL_DESC_DISPLAY_SIZE|Es el número máximo de caracteres necesario para mostrar los datos de la columna. Para columnas de tipos de valor grande, el valor devuelto es SQL_SS_LENGTH_UNLIMITED.|  
|SQL_DESC_LENGTH|Devuelve la longitud real de la columna en el conjunto de resultados. Para columnas de tipos de valor grande, el valor devuelto es SQL_SS_LENGTH_UNLIMITED.|  
|SQL_DESC_OCTET_LENGTH|Devuelve la longitud máxima de una columna de tipos de valor grande. SQL_SS_LENGTH_UNLIMITED se usa para indicar un tamaño ilimitado.|  
|SQL_DESC_PRECISION|Para columnas de tipos de valor grande, devuelve el valor SQL_SS_LENGTH_UNLIMITED.|  
|SQL_DESC_TYPE|Devuelve SQL_VARCHAR, SQL_WVARCHAR y SQL_VARBINARY para tipos de valor grande.|  
|SQL_DESC_TYPE_NAME|Devuelve "varchar", "varbinary" y "nvarchar" para tipos de valor grande.|  
  
 Para todas las versiones, solo se notifican los atributos de columna del primer conjunto de resultados cuando un lote preparado de instrucciones SQL genera varios conjuntos de resultados.  
  
 Los siguientes atributos de columna son extensiones expuestas por el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client devuelve todos los valores del parámetro *NumericAttrPtr* . Los valores se devuelven como SDWORD (largo con signo) excepto SQL_CA_SS_COMPUTE_BYLIST, que es un puntero a una matriz WORD.  
  
|Identificador de campo|Valor devuelto|  
|----------------------|--------------------|  
|SQL_CA_SS_COLUMN_HIDDEN*|Es TRUE si la columna a la que se hace referencia forma parte de una clave principal oculta creada para admitir una instrucción SELECT de Transact-SQL que contiene FOR BROWSE.|  
|SQL_CA_SS_COLUMN_ID|Posición ordinal de la columna de resultados de una cláusula COMPUTE en la instrucción SELECT de Transact-SQL actual.|  
|SQL_CA_SS_COLUMN_KEY*|Es TRUE si la columna a la que se hace referencia forma parte de una clave principal de la fila y la instrucción SELECT de Transact-SQL contiene FOR BROWSE.|  
|SQL_CA_SS_COLUMN_OP|Entero que especifica el operador de agregado responsable del valor en una columna de la cláusula COMPUTE. Las definiciones de los valores enteros están en sqlncli.h.|  
|SQL_CA_SS_COLUMN_ORDER|Posición ordinal de la columna en la cláusula ORDER BY de una instrucción SELECT de Transact-SQL u ODBC.|  
|SQL_CA_SS_COLUMN_SIZE|Longitud máxima, en bytes, necesaria para enlazar un valor de datos recuperado de la columna a una variable SQL_C_BINARY.|  
|SQL_CA_SS_COLUMN_SSTYPE|Tipo de datos nativo de los datos almacenados en la columna de SQL Server. Las definiciones de los valores de tipo están en sqlncli.h.|  
|SQL_CA_SS_COLUMN_UTYPE|Tipo de datos base del tipo de datos definidos por el usuario de la columna de SQL Server. Las definiciones de los valores de tipo están en sqlncli.h.|  
|SQL_CA_SS_COLUMN_VARYLEN|Es TRUE si los datos de la columna pueden variar en longitud; de lo contrario, es FALSE.|  
|SQL_CA_SS_COMPUTE_BYLIST|Puntero a una matriz de WORD (corto sin signo) que especifica las columnas que se usan en la frase BY de una cláusula COMPUTE. Si la cláusula COMPUTE no especifica ninguna frase BY, se devuelve un puntero NULL.<br /><br /> El primer elemento de la matriz contiene el recuento de las columnas de la lista BY. Los demás elementos son los ordinales de columna.|  
|SQL_CA_SS_COMPUTE_ID|*computeid* de una fila que es el resultado de una cláusula COMPUTE de la instrucción SELECT de Transact-SQL actual.|  
|SQL_CA_SS_NUM_COMPUTES|Número de cláusulas COMPUTE especificadas en la instrucción SELECT de Transact-SQL actual.|  
|SQL_CA_SS_NUM_ORDERS|Número de columnas especificadas en la cláusula ORDER BY de una instrucción SELECT de Transact-SQL u ODBC.|  
  
 \*Available si el atributo de instrucción SQL_SOPT_SS_HIDDEN_COLUMNS está establecido en SQL_HC_ON.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]se introdujeron campos descriptores específicos del controlador para proporcionar información adicional para indicar el nombre de la colección de esquemas XML, el nombre de esquema y el nombre de catálogo, respectivamente. Estas propiedades no requieren comillas ni un carácter de escape si contienen caracteres no alfanuméricos. En la tabla siguiente se enumeran estos nuevos campos descriptores:  
  
|Nombre de la columna|Tipo|Descripción|  
|-----------------|----------|-----------------|  
|SQL_CA_SS_XML_SCHEMACOLLECTION_CATALOG_NAME|CharacterAttributePtr|Nombre del catálogo donde se define el nombre de una colección de esquemas XML. Si no se encuentra el nombre de catálogo, esta variable contiene una cadena vacía.<br /><br /> Esta información se devuelve del campo de registro SQL_DESC_SS_XML_SCHEMACOLLECTION_CATALOG_NAME de IRD, que es un campo de lectura y escritura.|  
|SQL_CA_SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|CharacterAttributePtr|Nombre del esquema donde se define el nombre de una colección de esquemas XML. Si no se encuentra el nombre de esquema, esta variable contiene una cadena vacía.<br /><br /> Esta información se devuelve del campo de registro SQL_DESC_SS_XML_SCHEMACOLLECTION_SCHEMA_NAME de IRD, que es un campo de lectura y escritura.|  
|SQL_CA_SS_XML_SCHEMACOLLECTION_NAME|CharacterAttributePtr|Nombre de una colección de esquemas XML. Si no se encuentra el nombre, esta variable contiene una cadena vacía.<br /><br /> Esta información se devuelve del campo de registro SQL_DESC_SS_XML_SCHEMACOLLECTION_NAME de IRD, que es un campo de lectura y escritura.|  
  
 Asimismo, en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] se introdujeron nuevos campos descriptores específicos del controlador para proporcionar información adicional para una columna de tipo definido por el usuario (UDT) de un conjunto de resultados o un parámetro UDT de un procedimiento almacenado o una consulta con parámetros. Estas propiedades no requieren comillas ni un carácter de escape si contienen caracteres no alfanuméricos. En la tabla siguiente se enumeran estos nuevos campos descriptores:  
  
|Nombre de columna|Tipo|Descripción|  
|-----------------|----------|-----------------|  
|SQL_CA_SS_UDT_CATALOG_NAME|CharacterAttributePtr|Nombre del catálogo que contiene el UDT.|  
|SQL_CA_SS_UDT_SCHEMA_NAME|CharacterAttributePtr|Nombre del esquema que contiene el UDT.|  
|SQL_CA_SS_UDT_TYPE_NAME|CharacterAttributePtr|Nombre del UDT.|  
|SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME|CharacterAttributePtr|Nombre completo de ensamblado del UDT.|  
  
 El identificador del campo descriptor SQL_DESC_TYPE_NAME existente se usa para indicar el nombre del UDT. El campo SQL_DESC_TYPE de una columna de tipo UDT es SQL_SS_UDT.  
  
## <a name="sqlcolattribute-support-for-enhanced-date-and-time-features"></a>Compatibilidad de SQLColAttribute con las características mejoradas de fecha y hora  
 Para los valores devueltos en los tipos de fecha y hora, vea la sección "Información que se devuelve en los campos IRD" de [Parameter and Result Metadata](../../relational-databases/native-client-odbc-date-time/metadata-parameter-and-result.md).  
  
 Para obtener más información, vea [mejoras de fecha y hora &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlcolattribute-support-for-large-clr-udts"></a>Compatibilidad de SQLColAttribute con UDT CLR grandes  
 **SQLColAttribute** admite tipos definidos por el usuario (UDT) CLR grandes. Para obtener más información, vea [tipos CLR grandes definidos por el usuario &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="sqlcolattribute-support-for-sparse-columns"></a>Compatibilidad de SQLColAttribute con columnas dispersas  
 SQLColAttribute consulta el nuevo campo de descriptor de fila de implementación (IRD), SQL_CA_SS_IS_COLUMN_SET, para determinar si una columna es una columna **COLUMN_SET** .  
  
 Para obtener más información, consulte [compatibilidad con columnas Dispersas &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md).  
  
## <a name="see-also"></a>Consulte también  
 [SQLColAttribute función)](https://go.microsoft.com/fwlink/?LinkId=59334)   
 [Detalles de implementación de la API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)  
  
  
