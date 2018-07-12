---
title: Actualizar una aplicación a SQL Server Native Client desde MDAC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
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
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0365cedaa710627b8dab6b2060c9c414f126cf99
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37428574"
---
# <a name="updating-an-application-to-sql-server-native-client-from-mdac"></a>Actualizar una aplicación de MDCA a SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Existen varias diferencias entre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client y Microsoft Data Access Components (MDAC; a partir de Windows Vista, los componentes de acceso a datos se denominan Data Access Components para Windows o DAC para Windows). Aunque ambos proporcionan acceso a datos nativos a las bases de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client está específicamente diseñado para exponer las nuevas características de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y, al mismo tiempo, mantener la compatibilidad con versiones anteriores.  
  
 La información de este tema puede servirle de ayuda para actualizar su aplicación MDAC (o Windows DAC) con la versión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que se incluía en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Para ayudarle a hacer que esta aplicación esté actualizada con la versión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que se incluye en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], consulte [actualizar una aplicación de SQL Server 2005 Native Client](../../../relational-databases/native-client/applications/updating-an-application-from-sql-server-2005-native-client.md).  
  
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
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no contiene integración con XML. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client admite la selección... PARA las consultas XML, pero no admite ninguna otra funcionalidad XML. Sin embargo, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client admite el **xml** tipo de datos que se introdujo en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client admite la configuración de bibliotecas de red del lado cliente solamente mediante el uso de atributos de cadena de conexión. Si necesita una configuración de biblioteca de red más completa, debe usar el Administrador de configuración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no es compatible con odbcbcp.dll. Las aplicaciones que usan ODBC y **bcp** API deben volver a generarse para vincularse con sqlncli11.lib para usar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no se admite desde el proveedor OLE DB de Microsoft para ODBC (MSDASQL). Si usa el controlador MDAC SQLODBC con MSDASQL o el controlador MDAC SQLODBC con ADO, use OLE DB en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
-   Las cadenas de conexión de MDAC permiten un valor booleano (**true**) para el **Trusted_Connection** palabra clave. Un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] debe usar la cadena de conexión de cliente nativo **Sí** o **ningún**.  
  
-   Se han realizado pequeños cambios en los errores y advertencias. Ahora, los errores y advertencias que devuelve el servidor conservan la misma gravedad cuando se pasan a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Debe asegurarse de que ha probado de forma exhaustiva la aplicación si depende de la interceptación de determinados errores y advertencias.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client dispone de un sistema de comprobación de errores más estricto que MDAC, lo que significa que algunas aplicaciones que no se ajustan estrictamente a las especificaciones OLE DB y ODBC pueden comportarse de manera diferente. Por ejemplo, el proveedor SQLOLEDB no exigía la regla que indica que los nombres de parámetro deben comenzar por '@' para los parámetros de resultado, pero el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client sí que lo exige.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client se comporta de distinto modo que MDAC con respecto a las conexiones con errores. Por ejemplo, MDAC devuelve valores de propiedad almacenados en caché para una conexión con errores, mientras que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client notifica un error a la aplicación que realiza la llamada.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no genera eventos de Visual Studio Analyzer, sino que genera eventos de seguimiento de Windows.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no puede usarse con perfmon. Perfmon es una herramienta de Windows que solo puede utilizarse con los DSN que usan el controlador MDAC SQLODBC que se incluye con Windows.  
  
-   Cuando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client se conecta a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y versiones posteriores, el error de servidor 16947 se devuelve como SQL_ERROR. Este error se produce cuando una actualización o eliminación posicionada genera errores al actualizar o eliminar una fila. Con MDAC al conectarse a cualquier versión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], se devuelve el error de servidor 16947 como una advertencia (SQL_SUCCESS_WITH_INFO).  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client implementa el **IDBDataSourceAdmin** interfaz, que es una interfaz OLE DB opcional que no se implementaba previamente, pero solo el **CreateDataSource** opcional de este método se implementa la interfaz. [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
-   El proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client devuelve sinónimos en el conjunto de filas de esquema de TABLES y TABLE_INFO, con TABLE_TYPE establecido en SYNONYM.  
  
-   Los valores devueltos de tipo de datos **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **xml**, **udt**, o de otros tipos de objetos grandes no pueden devolverse a versiones de cliente anteriores a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Si desea usar estos tipos de datos como valores devueltos, debe usar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
-   MDAC permite ejecutar las instrucciones siguientes al inicio de transacciones manuales e implícitas, mientras que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no. Deben ejecutarse en modo de confirmación automática.  
  
    -   Todas las operaciones de texto completo (índice y catálogo DDL)  
  
    -   Todas las operaciones de base de datos (crear base de datos, modificar base de datos, quitar base de datos)  
  
    -   Reconfigurar  
  
    -   Apagar  
  
    -   Eliminar  
  
    -   Copia de seguridad  
  
-   Cuando las aplicaciones MDAC se conecten a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], los tipos de datos introducidos en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] se mostrarán como tipos de datos compatibles con [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)], tal y como se indica en la tabla siguiente.  
  
    |Tipo de SQL Server 2005|Tipo de SQL Server 2000|  
    |--------------------------|--------------------------|  
    |**ntext**|**text**|  
    |**nvarchar(max)**|**ntext**|  
    |**varbinary(max)**|**imagen**|  
    |**udt**|**varbinary**|  
    |**xml**|**ntext**|  
  
     Esta asignación de tipos afecta a los valores devueltos para los metadatos de columna. Por ejemplo, un **texto** columna tiene un tamaño máximo de 2.147.483.647, pero [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ODBC de Native Client notifica el tamaño máximo de **varchar (max)** columnas como SQL_SS_LENGTH_UNLIMITED y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]OLE DB de native Client notifica el tamaño máximo de **varchar (max)** 2.147.483.647 ó -1, dependiendo de la plataforma.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client permite la ambigüedad en las cadenas de conexión por motivos de compatibilidad con versiones anteriores (por ejemplo, algunas palabras clave pueden especificarse más de una vez y pueden permitirse palabras clave en conflicto cuya resolución se base en la posición o en la prioridad). En futuras versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no se permitirá la ambigüedad en las cadenas de conexión. Es recomendable modificar las aplicaciones a fin de usar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para eliminar cualquier dependencia de ambigüedad en las cadenas de conexión.  
  
-   Si usa una llamada ODBC u OLE DB para iniciar las transacciones, existe una diferencia de comportamiento entre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client y MDAC; las transacciones se iniciarán inmediatamente con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client mientras que, con MDAC, las transacciones se iniciarán después del primer acceso a la base de datos. Esto puede afectar al comportamiento de los procedimientos almacenados y lotes porque [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] requiere@TRANCOUNT sea el mismo después de un lote o procedimiento almacenado finaliza la ejecución estaba cuando se inició el lote o procedimiento almacenado.  
  
-   Con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, ITransactionLocal::BeginTransaction hará que una transacción se inicie inmediatamente. Con MDAC, el inicio de transacciones se retrasa hasta que la aplicación ejecuta una instrucción que requiere una transacción en modo de transacción implícita. Para obtener más información, vea [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../../t-sql/statements/set-implicit-transactions-transact-sql.md).  
  
-   Pueden producirse errores al usar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador Native Client con System.Data.Odbc para tener acceso a un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] equipo del servidor que expone nuevos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-tipos de datos específicos o características. System.Data.Odbc proporciona una implementación genérica de ODBC y, posteriormente, no expone funcionalidad específica del proveedor o extensiones. (El controlador de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client se ha actualizado para admitir de forma nativa las características más recientes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].) Para solucionar este problema, puede volver a MDAC o migrar a System.Data.SqlClient.  
  
 Tanto [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client como MDAC admiten el aislamiento de transacción de lectura confirmada mediante el uso de versiones de fila, pero solo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client admite el aislamiento de transacción de instantánea. (En términos de programación, el aislamiento de transacción de lectura confirmada con versiones de fila es igual que la transacción de lectura confirmada.)  
  
## <a name="see-also"></a>Vea también  
 [Generar aplicaciones con SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
