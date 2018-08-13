---
title: Usos de los parámetros con valores de tabla ODBC | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), scenarios
- ODBC, table-valued parameters
ms.assetid: f1b73932-4570-4a8a-baa0-0f229d9c32ee
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: cf88502393533627c2169fda30995832b11f955d
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39558505"
---
# <a name="uses-of-odbc-table-valued-parameters"></a>Usos de parámetros con valores de tabla de ODBC
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  En este tema se describen los principales escenarios de usuario para usar parámetros con valores de tabla con ODBC:  
  
-   Parámetro con valores de tabla con búferes con varias filas completamente enlazados (enviar datos como un TVP con todos los valores de la memoria)  
  
-   Parámetro con valores de tabla con transmisión de filas por secuencias (enviar datos como un TVP usando datos en ejecución)  
  
-   Recuperar metadatos de parámetros con valores de tabla desde el catálogo del sistema  
  
-   Recuperar metadatos de parámetros con valores de tabla para una instrucción preparada  
  
## <a name="table-valued-parameter-with-fully-bound-multirow-buffers-send-data-as-a-tvp-with-all-values-in-memory"></a>Parámetro con valores de tabla con búferes con varias filas completamente enlazados (enviar datos como un TVP con todos los valores de la memoria)  
 Cuando se utilizan con búferes con varias filas completamente enlazados, todos los valores de parámetro están disponibles en la memoria. Esto es típico, por ejemplo, de una transacción OLTP, en la que los parámetros con valores de tabla pueden empaquetarse en un único procedimiento almacenado. Sin parámetros con valores de tabla, esto implicaría generar dinámicamente un lote complejo de varias instrucciones o realizar varias llamadas al servidor.  
  
 El propio parámetro con valores de tabla se enlaza mediante el uso de [SQLBindParameter](http://go.microsoft.com/fwlink/?LinkId=59328) junto con los otros parámetros. Una vez que se han enlazado todos los parámetros, la aplicación establece el atributo de parámetro foco, SQL_SOPT_SS_PARAM_FOCUS, para cada parámetro con valores de tabla y llamadas SQLBindParameter para la columna del parámetro con valores de tabla.  
  
 El tipo de servidor de un parámetro con valores de tabla es un tipo nuevo específico de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SQL_SS_TABLE. El tipo C de enlace para SQL_SS_TABLE debe ser siempre SQL_C_DEFAULT. No se transfiere ningún dato para el parámetro enlazado al parámetro con valores de tabla; se usa para pasar metadatos de tabla y controlar la forma de pasar datos en las columnas constituyentes del parámetro con valores de tabla.  
  
 La longitud del parámetro con valores de tabla se establece en el número de filas que se envían al servidor. La *ColumnSize* parámetro de SQLBindParameter para un parámetro con valores de tabla especifica el número máximo de filas que se pueden enviar; este es el tamaño de los búferes de columna de la matriz. *ParameterValuePtr* es el parámetro de búfer, un parámetro con valores de tabla en SQLBindParameter. *ParameterValuePtr* y su asociado *BufferLength* se utilizan para pasar el nombre de tipo del parámetro con valores de tabla cuando sea necesario. El nombre de tipo no es necesario para las llamadas a procedimientos almacenados, pero sí para las instrucciones SQL.  
  
 Cuando se especifica un nombre de tipo del parámetro con valores de tabla en una llamada a SQLBindParameter, siempre debe especificarse como un valor Unicode, incluso en aplicaciones que se crean como aplicaciones de ANSI. Cuando se especifica un nombre de tipo del parámetro con valores de tabla mediante el uso de SQLSetDescField, puede utilizar un literal que se ajusta a la forma en que se basa la aplicación. El administrador de controladores ODBC realizará cualquier conversión Unicode que sea necesaria.  
  
 Metadatos de los parámetros con valores de tabla y columnas de parámetros con valores de tabla pueden manipularse individualmente y explícitamente utilizando SQLGetDescRec, SQLSetDescRec, SQLGetDescField y SQLSetDescField. Sin embargo, la sobrecarga SQLBindParameter suele ser más cómodo y no requiere explícita descriptor acceso en la mayoría de los casos. Este enfoque es coherente con la definición de SQLBindParameter para otros tipos de datos, excepto que para un parámetro con valores de tabla, los campos del descriptor afectados son ligeramente diferentes.  
  
 A veces, una aplicación usa un parámetro con valores de tabla con SQL dinámico y debe proporcionarse el nombre de tipo del parámetro con valores de tabla. Si es así y no está definido el parámetro con valores de tabla en el esquema predeterminado actual para la conexión, deben establecerse utilizando SQLSetDescField SQL_CA_SS_TYPE_CATALOG_NAME y SQL_CA_SS_TYPE_SCHEMA_NAME. Dado que las definiciones de tipo de tabla y los parámetros con valores de tabla deben estar en la misma base de datos, no debe establecerse SQL_CA_SS_TYPE_CATALOG_NAME si la aplicación utiliza parámetros con valores de tabla. De lo contrario, SQLSetDescField informará de un error.  
  
 Código de ejemplo de este escenario es en el procedimiento `demo_fixed_TVP_binding` en [Use Table-Valued parámetros &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md).  
  
## <a name="table-valued-parameter-with-row-streaming-send-data-as-a-tvp-using-data-at-execution"></a>Parámetro con valores de tabla con transmisión de filas por secuencias (enviar datos como un TVP usando datos en ejecución)  
 En este escenario, la aplicación proporciona filas al controlador a medida que éste las solicita y se transmiten por secuencias al servidor. Esto evita tener que almacenar en el búfer todas las filas de la memoria. Es representativo de los escenarios de inserción/actualización masiva. Los parámetros con valores de tabla proporcionan un punto de rendimiento en algún lugar entre las matrices de parámetros y la copia masiva. Es decir, los parámetros con valores de tabla son casi tan fáciles de programar como las matrices de parámetros, pero proporcionan mayor flexibilidad en el servidor.  
  
 El parámetro con valores de tabla y sus columnas se enlazan tal y como se explicó en la sección anterior, Parámetro con valores de tabla con búferes con varias filas completamente enlazados, pero el indicador de longitud del propio parámetro con valores de tabla se establece en SQL_DATA_AT_EXEC. El controlador responde a SQLExecute o SQLExecuteDirect de la forma habitual para los parámetros de datos en ejecución, es decir, devolviendo el valor SQL_NEED_DATA. Cuando el controlador está preparado para aceptar datos de un parámetro con valores de tabla, SQLParamData devuelve el valor de *ParameterValuePtr* en SQLBindParameter.  
  
 Una aplicación utiliza SQLPutData para un parámetro con valores de tabla para indicar la disponibilidad de los datos de las columnas de constituyentes de parámetro con valores de tabla. Cuando se llama a SQLPutData para un parámetro con valores de tabla, *DataPtr* siempre debe ser null y *StrLen_or_Ind* debe ser 0 o un número menor o igual que el tamaño de la matriz especificado de valores de tabla búferes de parámetros (el *ColumnSize* parámetro de SQLBindParameter). 0 significa que no hay más filas para el parámetro con valores de tabla y que el controlador pasará a procesar el siguiente parámetro de procedimiento real. Cuando *StrLen_or_Ind* es no es 0, el controlador procesará las columnas constituyentes del parámetro con valores de tabla de la misma manera como parámetro sin valor tabla de enlace de parámetros: cada columna del parámetro con valores de tabla puede especificar sus datos reales longitud, SQL_NULL_DATA o se pueden especificar datos en ejecución a través de su búfer de longitud/indicador. Columna del parámetro con valores de tabla se pueden pasar valores por las llamadas repetidas a SQLPutData como de costumbre cada vez un carácter o el valor binario a pasarse en trozos.  
  
 Cuando se han procesado todas las columnas de parámetro con valores de tabla, el controlador regresa al parámetro con valores de tabla para procesar más filas de datos de parámetro con valores de tabla. Por lo tanto, para los parámetros con valores de tabla de datos en ejecución, el controlador no sigue el examen secuencial habitual de los parámetros enlazados. Un parámetro con valores de tabla dependiente se examinarán hasta que se llame a SQLPutData con *StrLen_Or_IndPtr* igual a 0, momento en el que el controlador omite columnas de parámetros con valores de tabla y se mueve hacia el siguiente parámetro de procedimiento almacenado real.  Cuando SQLPutData pasa un valor de indicador mayor que o igual a 1, el controlador procesa las filas y columnas de parámetros con valores de tabla secuencialmente hasta que tiene valores para todas las filas enlazadas y columnas. A continuación, el controlador regresa al parámetro con valores de tabla. Entre la recepción del símbolo (token) para el parámetro con valores de tabla de SQLParamData y llamar a SQLPutData (hstmt, NULL, n) de un parámetro con valores de tabla, la aplicación debe establecer datos de columna constituyentes del parámetro con valores de tabla y el indicador de contenido de búfer para el fila o filas que se pasan al servidor siguiente.  
  
 Código de ejemplo de este escenario es en la rutina `demo_variable_TVP_binding` en [Use Table-Valued parámetros &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md).  
  
## <a name="retrieving-table-valued-parameter-metadata-from-the-system-catalog"></a>Recuperar metadatos de parámetros con valores de tabla desde el catálogo del sistema  
 Cuando una aplicación llama a un procedimiento que tiene parámetros de parámetro con valores de tabla SQLProcedureColumns, DATA_TYPE es devuelto como SQL_SS_TABLE y TYPE_NAME es el nombre del tipo de tabla del parámetro con valores de tabla. Se agregan dos columnas adicionales al conjunto de resultados devuelto por SQLProcedureColumns: SS_TYPE_CATALOG_NAME devuelve el nombre del catálogo donde se define el tipo de tabla del parámetro de valor de tabla y SS_TYPE_SCHEMA_NAME devuelve el nombre del esquema en el donde se define el tipo de tabla del parámetro de valor de tabla. De acuerdo con la especificación ODBC, SS_TYPE_CATALOG_NAME y SS_TYPE_SCHEMA_NAME aparecen antes que todas las columnas específicas del controlador agregadas en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y después de todas las columnas asignadas por el propio ODBC.  
  
 Las nuevas columnas no solo se rellenarán para los parámetros con valores de tabla, sino también para los parámetros de tipo definidos por el usuario CLR. El esquema y las columnas de catálogo existentes de los parámetros UDT también se rellenarán, pero al tener un esquema y columnas de catálogo comunes para los tipos de datos que los requieren, se simplificará el desarrollo futuro de aplicaciones. (Tenga en cuenta que las colecciones de esquemas XML son algo diferentes y no se incluyen en este cambio.)  
  
 Una aplicación utiliza SQLTables para determinar los nombres de tipos de tabla de la misma manera que lo hace para tablas persistentes, las vistas y tablas del sistema. Se ha introducido un nuevo tipo de tabla, TABLE TYPE, para permitir que una aplicación identifique los tipos de tabla asociados a parámetros con valores de tabla. Los tipos de tabla y las tablas normales usan espacios de nombres diferentes. Esto significa que puede utilizarse el mismo nombre tanto para un tipo de tabla como para una tabla real. Para administrar esto, se ha introducido un nuevo atributo de instrucción, SQL_SOPT_SS_NAME_SCOPE. Este atributo especifica si deben interpretar SQLTables y otras funciones de catálogo que toman un nombre de tabla como parámetro el nombre de la tabla como el nombre de una tabla real o el nombre de un tipo de tabla.  
  
 Una aplicación utiliza SQLColumns para determinar las columnas de un tipo de tabla de la misma manera que lo hace para tablas persistentes, pero primero debe establecer SQL_SOPT_SS_NAME_SCOPE para indicar que está trabajando con tipos de tabla en lugar de tablas reales. SQLPrimaryKeys también puede utilizarse con los tipos de tabla, con SQL_SOPT_SS_NAME_SCOPE.  
  
 Código de ejemplo de este escenario es en la rutina `demo_metadata_from_catalog_APIs` en [Use Table-Valued parámetros &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md).  
  
## <a name="retrieving-table-valued-parameter-metadata-for-a-prepared-statement"></a>Recuperar metadatos de parámetros con valores de tabla para una instrucción preparada  
 En este escenario, una aplicación utiliza SQLNumParameters y SQLDescribeParam para recuperar metadatos de los parámetros con valores de tabla.  
  
 El campo IPD SQL_CA_SS_TYPE_NAME se usa para recuperar el nombre de tipo del parámetro con valores de tabla. Los campos IPD SQL_CA_SS_TYPE_SCHEMA_NAME y SQL_CA_SS_TYPE_CATALOG_NAME se usan para recuperar su catálogo y su esquema, respectivamente.  
  
 Las definiciones de tipo de tabla y los parámetros con valores de tabla deben estar en la misma base de datos. SQLSetDescField notificará un error si una aplicación establece SQL_CA_SS_TYPE_CATALOG_NAME cuando se usan parámetros con valores de tabla.  
  
 SQL_CA_SS_TYPE_CATALOG_NAME y SQL_CA_SS_TYPE_SCHEMA_NAME también pueden utilizarse para recuperar el catálogo y el esquema asociados a parámetros de tipo definidos por el usuario CLR. SQL_CA_SS_TYPE_CATALOG_NAME y SQL_CA_SS_TYPE_SCHEMA_NAME son alternativas a los atributos existentes de esquema de catálogo específicos del tipo para tipos UDT CLR.  
  
 Una aplicación utiliza SQLColumns para recuperar metadatos de columna de un parámetro con valores de tabla en este escenario, demasiado, porque SQLDescribeParam no devolver los metadatos de las columnas de una columna del parámetro con valores de tabla.  
  
 Es el código de ejemplo para este caso de uso en la rutina `demo_metadata_from_prepared_statement` en [Use Table-Valued parámetros &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Vea también  
 [Parámetros con valores de tabla &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
