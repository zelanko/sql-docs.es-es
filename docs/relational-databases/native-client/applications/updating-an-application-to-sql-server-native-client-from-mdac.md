---
title: Native Client, actualizar la aplicación SQL desde MDAC
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- SQLNCLI, vs. MDAC
- SQL Server Native Client, vs. MDAC
- data access [SQL Server Native Client], vs. MDAC
- SQL Server Native Client, updating applications
ms.assetid: 2860efdd-c59a-4deb-8a0e-5124a8f4e6dd
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f8f6b7efd8d97f63e93061cbef1a54e1df3146d2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "75243788"
---
# <a name="updating-an-application-to-sql-server-native-client-from-mdac"></a>Actualizar una aplicación de MDCA a SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Existen varias diferencias entre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client y Microsoft Data Access Components (MDAC; a partir de Windows Vista, los componentes de acceso a datos se denominan Data Access Components para Windows o DAC para Windows). Aunque ambos proporcionan acceso a datos nativos a las bases de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client está específicamente diseñado para exponer las nuevas características de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y, al mismo tiempo, mantener la compatibilidad con versiones anteriores.  
  
 La información de este tema puede servirle de ayuda para actualizar su aplicación MDAC (o Windows DAC) con la versión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que se incluía en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Para ayudarle a hacer que esta aplicación esté actualizada con la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] versión de Native Client que [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]se incluye en, consulte [actualización de una aplicación desde SQL Server 2005 Native Client](../../../relational-databases/native-client/applications/updating-an-application-from-sql-server-2005-native-client.md).  
  
 Además, aunque MDAC contiene componentes para usar OLE DB, ODBC y objetos de datos ActiveX (ADO), [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client solamente implementa OLE DB y ODBC (aunque ADO puede tener acceso a la funcionalidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client).  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client y MDAC presentan diferencias en las áreas siguientes:  
  
-   Es posible que los usuarios que obtengan acceso a un proveedor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client mediante ADO encuentren menos funcionalidad de filtrado que cuando obtienen acceso a un proveedor OLE DB de SQL.  
  
-   Si una aplicación ADO usa [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e intenta actualizar una columna calculada, se notificará un error. Con MDAC, la actualización se acepta, pero se omite.  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client es un único archivo de biblioteca de vínculos dinámicos (DLL) independiente. Las interfaces que se exponen públicamente se han reducido al mínimo, tanto para facilitar la distribución como para limitar la exposición a riesgos de seguridad.  
  
-   Solo se admiten las interfaces ODBC y OLE DB.  
  
-   Los nombres del proveedor OLE DB y del controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client son distintos a los que se usan con MDAC.  
  
-   La funcionalidad accesible al usuario que proporcionan los componentes MDAC también está disponible cuando se usa [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Entre otras características, se incluyen las siguientes: agrupación de conexiones, compatibilidad con ADO y compatibilidad con cursores de cliente. Cuando se utiliza cualquiera de estas características, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client solamente proporciona conectividad de base de datos. MDAC proporciona funciones como seguimiento, controles de administración y contadores de rendimiento.  
  
-   Las aplicaciones pueden usar los servicios principales de OLE DB con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, pero si usan el motor de cursor de OLE DB, deben usar la opción de compatibilidad de tipo de datos para evitar cualquier problema que pudiera surgir debido a que el motor del cursor no tiene ningún conocimiento de los nuevos tipos de datos de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client admite el acceso a las bases de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores.  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no contiene integración con XML. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client admite SELECT... Consultas FOR XML, pero no admite ninguna otra funcionalidad XML. Sin embargo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , Native Client admite el tipo de datos **XML** introducido [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]en.  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client admite la configuración de bibliotecas de red del lado cliente solamente mediante el uso de atributos de cadena de conexión. Si necesita una configuración de biblioteca de red más completa, debe usar el Administrador de configuración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no es compatible con odbcbcp.dll. Las aplicaciones que usan las API de ODBC y **BCP** deben volver a generarse para vincularse con sqlncli11. lib [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para poder usar Native Client.  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no se admite desde el proveedor OLE DB de Microsoft para ODBC (MSDASQL). Si usa el controlador MDAC SQLODBC con MSDASQL o el controlador MDAC SQLODBC con ADO, use OLE DB en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
-   Las cadenas de conexión de MDAC permiten un valor booleano (**true**) para la palabra clave **Trusted_Connection** . Una [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cadena de conexión de cliente nativo debe utilizar **sí** o **no**.  
  
-   Se han realizado pequeños cambios en los errores y advertencias. Ahora, los errores y advertencias que devuelve el servidor conservan la misma gravedad cuando se pasan a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Debe asegurarse de que ha probado de forma exhaustiva la aplicación si depende de la interceptación de determinados errores y advertencias.  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client dispone de un sistema de comprobación de errores más estricto que MDAC, lo que significa que algunas aplicaciones que no se ajustan estrictamente a las especificaciones OLE DB y ODBC pueden comportarse de manera diferente. Por ejemplo, el proveedor SQLOLEDB no aplicó la regla de que los nombres de parámetro deben comenzar\@por ' ' para los parámetros de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] resultado, pero el proveedor de OLE DB de Native Client sí lo hace.  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client se comporta de distinto modo que MDAC con respecto a las conexiones con errores. Por ejemplo, MDAC devuelve valores de propiedad almacenados en caché para una conexión con errores, mientras que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client notifica un error a la aplicación que realiza la llamada.  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no genera eventos de Visual Studio Analyzer, sino que genera eventos de seguimiento de Windows.  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no puede usarse con perfmon. Perfmon es una herramienta de Windows que solo puede utilizarse con los DSN que usan el controlador MDAC SQLODBC que se incluye con Windows.  
  
-   Cuando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client se conecta a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y versiones posteriores, el error de servidor 16947 se devuelve como SQL_ERROR. Este error se produce cuando una actualización o eliminación posicionada genera errores al actualizar o eliminar una fila. Con MDAC al conectarse a cualquier versión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], se devuelve el error de servidor 16947 como una advertencia (SQL_SUCCESS_WITH_INFO).  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client implementa la interfaz **IDBDataSourceAdmin** , que es una interfaz de OLE DB opcional que no se implementó anteriormente, pero solo se implementa el método **CreateDataSource** de esta interfaz opcional. [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
-   El proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client devuelve sinónimos en el conjunto de filas de esquema de TABLES y TABLE_INFO, con TABLE_TYPE establecido en SYNONYM.  
  
-   Los valores devueltos de tipo de datos **VARCHAR (Max)**, **nvarchar (Max)**, **varbinary (Max)**, **XML**, **UDT**u otros tipos de objetos grandes no se pueden devolver a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]versiones de cliente anteriores a. Si desea usar estos tipos de datos como valores devueltos, debe usar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
-   MDAC permite ejecutar las instrucciones siguientes al inicio de transacciones manuales e implícitas, mientras que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no. Deben ejecutarse en modo de confirmación automática.  
  
    -   Todas las operaciones de texto completo (índice y catálogo DDL)  
  
    -   Todas las operaciones de base de datos (crear base de datos, modificar base de datos, quitar base de datos)  
  
    -   Volver a configurar  
  
    -   Shutdown  
  
    -   Terminar  
  
    -   Copia de seguridad  
  
-   Cuando las aplicaciones MDAC se conecten a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], los tipos de datos introducidos en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] se mostrarán como tipos de datos compatibles con [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)], tal y como se indica en la tabla siguiente.  
  
    |Tipo de SQL Server 2005|Tipo de SQL Server 2000|  
    |--------------------------|--------------------------|  
    |**ntext**|**negrita**|  
    |**nvarchar(max)**|**ntext**|  
    |**varbinary(max)**|**impresión**|  
    |**definido**|**varbinary**|  
    |**lenguaje**|**ntext**|  
  
     Esta asignación de tipos afecta a los valores devueltos para los metadatos de columna. Por ejemplo, una columna de **texto** tiene un tamaño máximo de 2.147.483.647, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pero ODBC de Native Client notifica el tamaño máximo de columnas **varchar (Max)** como SQL_SS_LENGTH_UNLIMITED [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y Native Client OLE DB notifica el tamaño máximo de las columnas **VARCHAR (Max)** como 2.147.483.647 o-1, dependiendo de la plataforma.  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client permite la ambigüedad en las cadenas de conexión por motivos de compatibilidad con versiones anteriores (por ejemplo, algunas palabras clave pueden especificarse más de una vez y pueden permitirse palabras clave en conflicto cuya resolución se base en la posición o en la prioridad). En futuras versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no se permitirá la ambigüedad en las cadenas de conexión. Es recomendable modificar las aplicaciones a fin de usar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para eliminar cualquier dependencia de ambigüedad en las cadenas de conexión.  
  
-   Si usa una llamada ODBC u OLE DB para iniciar las transacciones, existe una diferencia de comportamiento entre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client y MDAC; las transacciones se iniciarán inmediatamente con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client mientras que, con MDAC, las transacciones se iniciarán después del primer acceso a la base de datos. Esto puede afectar al comportamiento de los procedimientos almacenados y los lotes [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] porque \@ \@requiere que TRANCOUNT sea el mismo después de que un lote o un procedimiento almacenado termine la ejecución tal como estaba cuando se inició el lote o el procedimiento almacenado.  
  
-   Con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, ITransactionLocal:: BeginTransaction hará que una transacción se inicie inmediatamente. Con MDAC, el inicio de transacciones se retrasa hasta que la aplicación ejecuta una instrucción que requiere una transacción en modo de transacción implícita. Para obtener más información, vea [SET IMPLICIT_TRANSACTIONS &#40;&#41;de Transact-SQL ](../../../t-sql/statements/set-implicit-transactions-transact-sql.md).  
  
-   Podría encontrar errores al usar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] el controlador de Native Client con System. Data. ODBC para tener [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] acceso a un equipo servidor que exponga [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]nuevas características o tipos de datos específicos de. System. Data. ODBC proporciona una implementación genérica de ODBC y, posteriormente, no expone ninguna funcionalidad o extensión específica del proveedor. (El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador de Native Client se actualiza para admitir de forma nativa [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] las características más recientes). Para solucionar este problema, puede revertir a MDAC o migrar a System. Data. SqlClient.  
  
 Tanto [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client como MDAC admiten el aislamiento de transacción de lectura confirmada mediante el uso de versiones de fila, pero solo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client admite el aislamiento de transacción de instantánea. (En términos de programación, el aislamiento de transacción de lectura confirmada con versiones de fila es igual que la transacción de lectura confirmada.)  
  
## <a name="see-also"></a>Consulte también  
 [Generar aplicaciones con SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
