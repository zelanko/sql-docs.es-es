---
title: Actualización de MDAC
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e1651eecd3238f737adfe82cfef0d574b5312b6c
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388275"
---
# <a name="updating-an-application-to-sql-server-native-client-from-mdac"></a>Actualizar una aplicación de MDCA a SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Existen varias diferencias entre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client y Microsoft Data Access Components (MDAC; a partir de Windows Vista, los componentes de acceso a datos se denominan Data Access Components para Windows o DAC para Windows). Aunque ambos proporcionan acceso a datos nativos a las bases de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client está específicamente diseñado para exponer las nuevas características de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y, al mismo tiempo, mantener la compatibilidad con versiones anteriores.  
  
 La información de este tema puede servirle de ayuda para actualizar su aplicación MDAC (o Windows DAC) con la versión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que se incluía en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Para ayudarle a que esta aplicación [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sea actual con [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]la versión de Native Client que se incluye en , vea [Actualización de una aplicación desde SQL Server 2005 Native Client](../../../relational-databases/native-client/applications/updating-an-application-from-sql-server-2005-native-client.md).  
  
 Además, aunque MDAC contiene componentes para usar OLE DB, ODBC y objetos de datos ActiveX (ADO), [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client solamente implementa OLE DB y ODBC (aunque ADO puede tener acceso a la funcionalidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client y MDAC presentan diferencias en las áreas siguientes:  
  
-   Es posible que los usuarios que obtengan acceso a un proveedor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client mediante ADO encuentren menos funcionalidad de filtrado que cuando obtienen acceso a un proveedor OLE DB de SQL.  
  
-   Si una aplicación ADO usa [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e intenta actualizar una columna calculada, se notificará un error. Con MDAC, la actualización se acepta, pero se omite.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client es un único archivo de biblioteca de vínculos dinámicos (DLL) independiente. Las interfaces que se exponen públicamente se han reducido al mínimo, tanto para facilitar la distribución como para limitar la exposición a riesgos de seguridad.  
  
-   Solo se admiten las interfaces ODBC y OLE DB.  
  
-   Los nombres del proveedor OLE DB y del controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client son distintos a los que se usan con MDAC.  
  
-   La funcionalidad accesible al usuario que proporcionan los componentes MDAC también está disponible cuando se usa [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Entre otras características, se incluyen las siguientes: agrupación de conexiones, compatibilidad con ADO y compatibilidad con cursores de cliente. Cuando se utiliza cualquiera de estas características, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client solamente proporciona conectividad de base de datos. MDAC proporciona funciones como seguimiento, controles de administración y contadores de rendimiento.  
  
-   Las aplicaciones pueden usar los servicios principales de OLE DB con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, pero si usan el motor de cursor de OLE DB, deben usar la opción de compatibilidad de tipo de datos para evitar cualquier problema que pudiera surgir debido a que el motor del cursor no tiene ningún conocimiento de los nuevos tipos de datos de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client admite el acceso a las bases de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no contiene integración con XML. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client admite SELECT ... FOR XML consulta, pero no admite ninguna otra funcionalidad XML. Sin [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] embargo, Native Client admite el [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]tipo de datos **xml** introducido en .  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client admite la configuración de bibliotecas de red del lado cliente solamente mediante el uso de atributos de cadena de conexión. Si necesita una configuración de biblioteca de red más completa, debe usar el Administrador de configuración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no es compatible con odbcbcp.dll. Las aplicaciones que usan ODBC y las API **bcp** deben volver a generarse [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para vincularse con sqlncli11.lib para poder usar Native Client.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no se admite desde el proveedor OLE DB de Microsoft para ODBC (MSDASQL). Si usa el controlador MDAC SQLODBC con MSDASQL o el controlador MDAC SQLODBC con ADO, use OLE DB en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
-   Las cadenas de conexión de MDAC permiten un valor booleano (**true**) para la palabra clave **Trusted_Connection**. Una [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cadena de conexión de Native Client debe usar **yes** o **no**.  
  
-   Se han realizado pequeños cambios en los errores y advertencias. Ahora, los errores y advertencias que devuelve el servidor conservan la misma gravedad cuando se pasan a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Debe asegurarse de que ha probado de forma exhaustiva la aplicación si depende de la interceptación de determinados errores y advertencias.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client dispone de un sistema de comprobación de errores más estricto que MDAC, lo que significa que algunas aplicaciones que no se ajustan estrictamente a las especificaciones OLE DB y ODBC pueden comportarse de manera diferente. Por ejemplo, el proveedor SQLOLEDB no forzó la\@regla de que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] los nombres de parámetro deben comenzar con ' ' para los parámetros de resultado, pero sí lo hace el proveedor OLE DB de Native Client.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client se comporta de distinto modo que MDAC con respecto a las conexiones con errores. Por ejemplo, MDAC devuelve valores de propiedad almacenados en caché para una conexión con errores, mientras que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client notifica un error a la aplicación que realiza la llamada.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no genera eventos de Visual Studio Analyzer, sino que genera eventos de seguimiento de Windows.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no puede usarse con perfmon. Perfmon es una herramienta de Windows que solo puede utilizarse con los DSN que usan el controlador MDAC SQLODBC que se incluye con Windows.  
  
-   Cuando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client se conecta a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y versiones posteriores, el error de servidor 16947 se devuelve como SQL_ERROR. Este error se produce cuando una actualización o eliminación posicionada genera errores al actualizar o eliminar una fila. Con MDAC al conectarse a cualquier versión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], se devuelve el error de servidor 16947 como una advertencia (SQL_SUCCESS_WITH_INFO).  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client implementa la interfaz **IDBDataSourceAdmin,** que es una interfaz OLE DB opcional que no se implementó anteriormente, pero solo se implementa el método **CreateDataSource** de esta interfaz opcional. [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
-   El proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client devuelve sinónimos en el conjunto de filas de esquema de TABLES y TABLE_INFO, con TABLE_TYPE establecido en SYNONYM.  
  
-   Los valores devueltos del tipo de datos **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, **xml**, [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] **udt**u otros tipos de objetos grandes no se pueden devolver a versiones de cliente anteriores a . Si desea usar estos tipos de datos como valores devueltos, debe usar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
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
    |**varchar(max)**|**text**|  
    |**nvarchar(max)**|**ntext**|  
    |**varbinary(max)**|**Imagen**|  
    |**Udt**|**varbinary**|  
    |**xml**|**ntext**|  
  
     Esta asignación de tipos afecta a los valores devueltos para los metadatos de columna. Por ejemplo, una columna de **texto** tiene un tamaño máximo de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2.147.483.647, pero ODBC de Native Client notifica el tamaño máximo de las columnas **varchar(max)** como SQL_SS_LENGTH_UNLIMITED, y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB de Native Client notifica el tamaño máximo de las columnas **varchar(max)** como 2.147.483.647 o -1, dependiendo de la plataforma.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client permite la ambigüedad en las cadenas de conexión por motivos de compatibilidad con versiones anteriores (por ejemplo, algunas palabras clave pueden especificarse más de una vez y pueden permitirse palabras clave en conflicto cuya resolución se base en la posición o en la prioridad). En futuras versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no se permitirá la ambigüedad en las cadenas de conexión. Es recomendable modificar las aplicaciones a fin de usar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para eliminar cualquier dependencia de ambigüedad en las cadenas de conexión.  
  
-   Si usa una llamada ODBC u OLE DB para iniciar las transacciones, existe una diferencia de comportamiento entre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client y MDAC; las transacciones se iniciarán inmediatamente con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client mientras que, con MDAC, las transacciones se iniciarán después del primer acceso a la base de datos. Esto puede afectar al comportamiento de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] los \@ \@procedimientos almacenados y lotes porque requiere que TRANCOUNT sea el mismo después de que un lote o procedimiento almacenado finalice la ejecución que cuando se inició el lote o el procedimiento almacenado.  
  
-   Con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, ITransactionLocal::BeginTransaction hará que una transacción se inicie inmediatamente. Con MDAC, el inicio de transacciones se retrasa hasta que la aplicación ejecuta una instrucción que requiere una transacción en modo de transacción implícita. Para obtener más información, vea [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../../t-sql/statements/set-implicit-transactions-transact-sql.md).  
  
-   Es posible que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se produzcan errores al usar el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador de Native [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Client con System.Data.Odbc para tener acceso a un equipo servidor que expone características o tipos de datos nuevos y específicos. System.Data.Odbc proporciona una implementación ODBC genérica y, posteriormente, no expone la funcionalidad o las extensiones específicas del proveedor. (El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador de Native Client se [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] actualiza para admitir de forma nativa las características más recientes.) Para solucionar este problema, puede revertir a MDAC o migrar a System.Data.SqlClient.  
  
 Tanto [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client como MDAC admiten el aislamiento de transacción de lectura confirmada mediante el uso de versiones de fila, pero solo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client admite el aislamiento de transacción de instantánea. (En términos de programación, el aislamiento de transacción de lectura confirmada con versiones de fila es igual que la transacción de lectura confirmada.)  
  
## <a name="see-also"></a>Consulte también  
 [Generar aplicaciones con SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
