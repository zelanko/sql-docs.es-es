---
title: Actualización de una aplicación al controlador OLE DB para SQL Server desde MDAC | Microsoft Docs
description: Actualización de una aplicación al controlador OLE DB para SQL Server desde MDAC
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- MSOLEDBSQL, vs. MDAC
- OLE DB Driver for SQL Server, vs. MDAC
- data access [OLE DB Driver for SQL Server], vs. MDAC
- OLE DB Driver for SQL Server, updating applications
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 94e7db522cca98bf04cdb46ced06eb469e2cd1a6
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86007028"
---
# <a name="updating-an-application-to-ole-db-driver-for-sql-server-from-mdac"></a>Actualización de una aplicación al controlador OLE DB para SQL Server desde MDAC
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Existen varias diferencias entre el controlador OLE DB para SQL Server y Componentes de Microsoft Data Access (MDAC); a partir de Windows Vista, los componentes de acceso a datos se denominan Componentes de Windows Data Access (o Windows DAC). Aunque ambos proporcionan acceso de datos nativo a las bases de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], el controlador OLE DB para SQL Server se ha diseñado para exponer las nuevas características de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y, al mismo tiempo, mantener la compatibilidad con versiones anteriores.   

 Además, aunque MDAC contiene componentes para usar OLE DB, ODBC y objetos de datos ActiveX (ADO), OLE DB Driver for SQL Server solamente implementa OLE DB y ODBC (aunque ADO puede acceder a la funcionalidad de OLE DB Driver for SQL Server).  

 OLE DB Driver for SQL Server y MDAC presentan diferencias en las áreas siguientes:  

-   Es posible que los usuarios que accedan a un proveedor de OLE DB Driver for SQL Server mediante ADO encuentren menos funcionalidad de filtrado que cuando obtienen acceso a un proveedor OLE DB de SQL.  

-   Si una aplicación ADO usa OLE DB Driver for SQL Server e intenta actualizar una columna calculada, se notificará un error. Con MDAC, la actualización se acepta, pero se omite.  

-   OLE DB Driver for SQL Server es un único archivo de biblioteca de vínculos dinámicos (DLL) independiente. Las interfaces que se exponen públicamente se han reducido al mínimo, tanto para facilitar la distribución como para limitar la exposición a riesgos de seguridad.  

-   Solo se admiten las interfaces OLE DB.  

-   Los nombres de OLE DB Driver for SQL Server es diferente de los nombres que se usan con MDAC.  

-   La funcionalidad accesible al usuario que proporcionan los componentes MDAC también está disponible cuando se usa OLE DB Driver for SQL Server. Entre otras características, se incluyen las siguientes: agrupación de conexiones, compatibilidad con ADO y compatibilidad con cursores de cliente. Cuando se utiliza cualquiera de estas características, OLE DB Driver for SQL Server solamente proporciona conectividad de base de datos. MDAC proporciona funciones como seguimiento, controles de administración y contadores de rendimiento.  

-   Las aplicaciones pueden usar los servicios principales de OLE DB con el controlador OLE DB para SQL Server, pero si se usa el motor de cursores de OLE DB, deben usar la opción de compatibilidad de tipo de datos para evitar cualquier problema que pudiera surgir debido al desconocimiento de los nuevos tipos de datos de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] por parte del motor de cursores.  

-   OLE DB Driver for SQL Server admite el acceso a las bases de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores.  

-   OLE DB Driver for SQL Server no contiene integración con XML. OLE DB Driver for SQL Server admite las consultas SELECT... FOR XML, pero no admite ninguna otra funcionalidad XML. Sin embargo, OLE DB Driver for SQL Server admite el tipo de datos **xml** introducido en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  

-   El controlador OLE DB para SQL Server admite la configuración de bibliotecas de red de cliente mediante atributos de cadena de conexión solamente. Si necesita una configuración de biblioteca de red más completa, debe usar el Administrador de configuración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  

-   Las cadenas de conexión de MDAC permiten un valor booleano (**true**) para la palabra clave **Trusted_Connection**. Una cadena de conexión de OLE DB Driver for SQL Server debe usar **sí** o **no**.  

-   Se han realizado pequeños cambios en los errores y advertencias. Ahora, los errores y las advertencias que devuelve el servidor conservan la misma gravedad cuando se pasan al controlador OLE DB para SQL Server. Debe asegurarse de que ha probado de forma exhaustiva la aplicación si depende de la interceptación de determinados errores y advertencias.  

-   El controlador OLE DB para SQL Server dispone de un sistema de comprobación de errores más estricto que MDAC, lo que significa que algunas aplicaciones que no se ajustan estrictamente a las especificaciones de OLE DB pueden comportarse de manera diferente. Por ejemplo, el proveedor SQLOLEDB no exigía la regla consistente en que los nombres de parámetro deben comenzar por "\@" para los parámetros de resultado, pero el controlador OLE DB de SQL Server sí.  

-   OLE DB Driver for SQL Server se comporta de forma diferente a MDAC con respecto a las conexiones con error. Por ejemplo, MDAC devuelve valores de propiedad almacenados en caché para una conexión con errores, mientras que el controlador OLE DB para SQL Server notifica un error a la aplicación que realiza la llamada.  

-   El controlador OLE DB para SQL Server no genera eventos de Visual Studio Analyzer, sino eventos de seguimiento de Windows.  

-   No se puede usar OLE DB Driver for SQL Server con Perfmon. Perfmon es una herramienta de Windows que solo puede utilizarse con los DSN que usan el controlador MDAC SQLODBC que se incluye con Windows.  

-   Cuando OLE DB Driver for SQL Server se conecta a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y versiones posteriores, el error de servidor 16947 se devuelve como SQL_ERROR. Este error se produce cuando una actualización o eliminación posicionada genera errores al actualizar o eliminar una fila. Con MDAC al conectarse a cualquier versión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], se devuelve el error de servidor 16947 como una advertencia (SQL_SUCCESS_WITH_INFO).  

-   El controlador OLE DB para SQL Server implementa la interfaz **IDBDataSourceAdmin**, que es una interfaz opcional de OLE DB que no se implementaba anteriormente, aunque solo se implementa el método **CreateDataSource** de esta interfaz opcional. [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  

-   El controlador OLE DB para SQL Server devuelve sinónimos en los conjuntos de filas de esquema TABLES y TABLE_INFO, con TABLE_TYPE establecido en SYNONYM.  

-   Los valores devueltos de tipo de datos **varchar(max)** , **nvarchar(max)** , **varbinary(max)** , **xml**, **udt** u otros tipos de objetos grandes no pueden devolverse a versiones de cliente anteriores a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Si desea usar estos tipos de datos como valores devueltos, debe usar OLE DB Driver for SQL Server.  

-   MDAC permite ejecutar las instrucciones siguientes al inicio de transacciones manuales e implícitas, mientras que el controlador OLE DB para SQL Server no. Deben ejecutarse en modo de confirmación automática.  

    -   Todas las operaciones de texto completo (índice y catálogo DDL)  

    -   Todas las operaciones de base de datos (crear base de datos, modificar base de datos, quitar base de datos)  

    -   Volver a configurar  

    -   Shutdown  

    -   Terminar  

    -   Copia de seguridad  

-   Cuando las aplicaciones MDAC se conecten a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], los tipos de datos introducidos en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] se mostrarán como tipos de datos compatibles con [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)], tal y como se indica en la tabla siguiente.  

    |Tipo de SQL Server 2005|Tipo de SQL Server 2000|  
    |--------------------------|--------------------------|  
    |**ntext**|**text**|  
    |**nvarchar(max)**|**ntext**|  
    |**varbinary(max)**|**image**|  
    |**udt**|**varbinary**|  
    |**xml**|**ntext**|  

     Esta asignación de tipos afecta a los valores devueltos para los metadatos de columna. Por ejemplo, una columna de **texto** tiene un tamaño máximo de 2 147 483 647, pero OLE DB Driver for SQL Server informa del tamaño máximo de columnas **varchar(max)** como 2 147 483 647 o -1, dependiendo de la plataforma.  

-   El controlador OLE DB para SQL Server permite la ambigüedad en las cadenas de conexión por motivos de compatibilidad con versiones anteriores (por ejemplo, algunas palabras clave pueden especificarse más de una vez y pueden permitirse palabras clave en conflicto cuya resolución se base en la posición o en la precedencia). En futuras versiones de OLE DB Driver for SQL Server no se permitirán ambigüedades en las cadenas de conexión. Al modificar aplicaciones, es recomendable usar el controlador OLE DB para SQL Server a fin de eliminar cualquier dependencia sobre la ambigüedad de las cadenas de conexión.  

-   Si usa una llamada OLE DB para iniciar las transacciones, existe una diferencia de comportamiento entre OLE DB Driver for SQL Server y MDAC; las transacciones se iniciarán inmediatamente con OLE DB Driver for SQL Server mientras que, con MDAC, las transacciones se iniciarán después del primer acceso a la base de datos. Esto puede afectar al comportamiento de los procedimientos almacenados y los lotes porque [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] exige que @@TRANCOUNT sea igual una vez que finaliza la ejecución de un procedimiento almacenado o un lote que cuando se inició el lote o el procedimiento almacenado.  

-   Con OLE DB Driver for SQL Server, ITransactionLocal::BeginTransaction hará que una transacción se inicie de inmediato. Con MDAC, el inicio de una transacción se retrasa hasta que la aplicación ejecuta una instrucción que requiere una transacción en modo de transacción implícita. Para obtener más información, vea [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../../t-sql/statements/set-implicit-transactions-transact-sql.md).  


 Tanto OLE DB Driver for SQL Server como MDAC admiten el aislamiento de transacciones de lectura confirmada mediante las versiones de fila, pero solo OLE DB Driver for SQL Server admite el aislamiento de transacciones de instantáneas. (En términos de programación, el aislamiento de transacción de lectura confirmada con versiones de fila es igual que la transacción de lectura confirmada.)  

## <a name="see-also"></a>Consulte también  
 [Compilación de aplicaciones con el controlador OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
