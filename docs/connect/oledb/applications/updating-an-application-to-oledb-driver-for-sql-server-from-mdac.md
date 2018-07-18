---
title: Actualización de una aplicación al controlador OLE DB para SQL Server desde MDAC | Microsoft Docs
description: Actualización de una aplicación al controlador OLE DB para SQL Server desde MDAC
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- MSOLEDBSQL, vs. MDAC
- OLE DB Driver for SQL Server, vs. MDAC
- data access [OLE DB Driver for SQL Server], vs. MDAC
- OLE DB Driver for SQL Server, updating applications
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 6b2c3ba7bc7ea16a4079cb247b4e7159b40eeb1a
ms.sourcegitcommit: 5152caf8f4346f8b565742bc1df4e454551d63eb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/27/2018
ms.locfileid: "37042675"
---
# <a name="updating-an-application-to-ole-db-driver-for-sql-server-from-mdac"></a>Actualización de una aplicación al controlador OLE DB para SQL Server desde MDAC
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Existen varias diferencias entre el controlador OLE DB para SQL Server y Componentes de Microsoft Data Access (MDAC); a partir de Windows Vista, los componentes de acceso a datos se denominan Componentes de Windows Data Access (o Windows DAC). Aunque ambos proporcionan acceso de datos nativo a las bases de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], el controlador OLE DB para SQL Server se ha diseñado para exponer las nuevas características de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y, al mismo tiempo, mantener la compatibilidad con versiones anteriores.   

 Además, aunque MDAC contiene componentes para el uso de ActiveX Data Objects (ADO), OLE DB y ODBC, controlador de OLE DB para SQL Server sólo implementa OLE DB (aunque ADO puede tener acceso a la funcionalidad del controlador de OLE DB para SQL Server).  

 Controlador OLE DB para SQL Server y MDAC difieren en las siguientes áreas:  

-   Los usuarios que utilizar ADO para obtener acceso al controlador de OLE DB para SQL Server pueden encontrar menos funcionalidad de filtrado que cuando obtienen acceso al proveedor OLE DB de SQL.  

-   Si una aplicación ADO utiliza el controlador de OLE DB para SQL Server y se intenta actualizar una columna calculada, se notificará un error. Con MDAC, la actualización se acepta, pero se omite.  

-   Controlador OLE DB para SQL Server es un archivo de biblioteca (DLL) única vínculos dinámicos independientes. Las interfaces que se exponen públicamente se han reducido al mínimo, tanto para facilitar la distribución como para limitar la exposición a riesgos de seguridad.  

-   Se admiten sólo las interfaces de OLE DB.  

-   El controlador OLE DB para los nombres de SQL Server son diferentes de nombres que se usan con MDAC.  

-   Funcionalidad accesible para el usuario proporcionada por los componentes MDAC está disponible cuando se usa el controlador de OLE DB para SQL Server. Entre otras características, se incluyen las siguientes: agrupación de conexiones, compatibilidad con ADO y compatibilidad con cursores de cliente. Cuando se utiliza cualquiera de estas características, controlador OLE DB para SQL Server proporciona conectividad de base de datos solo. MDAC proporciona funciones como seguimiento, controles de administración y contadores de rendimiento.  

-   Las aplicaciones pueden usar los servicios principales de OLE DB con el controlador OLE DB para SQL Server, pero si se usa el motor de cursores de OLE DB, deben usar la opción de compatibilidad de tipo de datos para evitar cualquier problema que pudiera surgir debido al desconocimiento de los nuevos tipos de datos de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] por parte del motor de cursores.  

-   Controlador OLE DB para SQL Server admite el acceso a la anterior [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] bases de datos.  

-   Controlador OLE DB para SQL Server no tiene integración de XML. Controlador OLE DB para SQL Server admite la selección... PARA las consultas XML, pero no admite ninguna otra funcionalidad XML. Sin embargo, controlador de OLE DB para SQL Server admite la **xml** tipo de datos que se introdujo en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  

-   El controlador OLE DB para SQL Server admite la configuración de bibliotecas de red de cliente mediante atributos de cadena de conexión solamente. Si necesita una configuración de biblioteca de red más completa, debe usar el Administrador de configuración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  

-   Las cadenas de conexión de MDAC permiten un valor booleano (**true**) para el **Trusted_Connection** palabra clave. Debe usar un controlador de OLE DB para la cadena de conexión de SQL Server **Sí** o **ningún**.  

-   Se han realizado pequeños cambios en los errores y advertencias. Ahora, los errores y las advertencias que devuelve el servidor conservan la misma gravedad cuando se pasan al controlador OLE DB para SQL Server. Debe asegurarse de que ha probado de forma exhaustiva la aplicación si depende de la interceptación de determinados errores y advertencias.  

-   El controlador OLE DB para SQL Server dispone de un sistema de comprobación de errores más estricto que MDAC, lo que significa que algunas aplicaciones que no se ajustan estrictamente a las especificaciones de OLE DB pueden comportarse de manera diferente. Por ejemplo, el proveedor SQLOLEDB no exigía la regla consistente en que los nombres de parámetro deben comenzar por "\@" para los parámetros de resultado, pero el controlador OLE DB de SQL Server sí.  

-   Controlador OLE DB para SQL Server se comporta de forma diferente de MDAC con respecto a las conexiones con errores. Por ejemplo, MDAC devuelve valores de propiedad almacenados en caché para una conexión con errores, mientras que el controlador OLE DB para SQL Server notifica un error a la aplicación que realiza la llamada.  

-   El controlador OLE DB para SQL Server no genera eventos de Visual Studio Analyzer, sino eventos de seguimiento de Windows.  

-   Controlador OLE DB para SQL Server no puede usarse con perfmon. Perfmon es una herramienta de Windows que solo puede utilizarse con los DSN que usan el controlador MDAC SQLODBC que se incluye con Windows.  

-   Cuando está conectado el controlador OLE DB para SQL Server a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y versiones posteriores, el error de servidor 16947 se devuelve como SQL_ERROR. Este error se produce cuando una actualización o eliminación posicionada genera errores al actualizar o eliminar una fila. Con MDAC al conectarse a cualquier versión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], se devuelve el error de servidor 16947 como una advertencia (SQL_SUCCESS_WITH_INFO).  

-   El controlador OLE DB para SQL Server implementa la interfaz **IDBDataSourceAdmin**, que es una interfaz opcional de OLE DB que no se implementaba anteriormente, aunque solo se implementa el método **CreateDataSource** de esta interfaz opcional. [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  

-   El controlador OLE DB para SQL Server devuelve sinónimos en los conjuntos de filas de esquema TABLES y TABLE_INFO, con TABLE_TYPE establecido en SYNONYM.  

-   Los valores devueltos de tipo de datos **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, **xml**, **udt** u otros tipos de objetos grandes no pueden devolverse a versiones de cliente anteriores a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Si desea usar estos tipos como valores devueltos, debe usar el controlador de OLE DB para SQL Server.  

-   MDAC permite ejecutar las instrucciones siguientes al inicio de transacciones manuales e implícitas, mientras que el controlador OLE DB para SQL Server no. Deben ejecutarse en modo de confirmación automática.  

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

     Esta asignación de tipos afecta a los valores devueltos para los metadatos de columna. Por ejemplo, un **texto** columna tiene un tamaño máximo de 2.147.483.647, pero el controlador OLE DB para SQL Server informa del tamaño máximo de **varchar (max)** 2.147.483.647 ó -1, dependiendo de la plataforma.  

-   El controlador OLE DB para SQL Server permite la ambigüedad en las cadenas de conexión por motivos de compatibilidad con versiones anteriores (por ejemplo, algunas palabras clave pueden especificarse más de una vez y pueden permitirse palabras clave en conflicto cuya resolución se base en la posición o en la precedencia). Futuras versiones del controlador OLE DB para SQL Server no es posible que permitirá la ambigüedad en las cadenas de conexión. Al modificar aplicaciones, es recomendable usar el controlador OLE DB para SQL Server a fin de eliminar cualquier dependencia sobre la ambigüedad de las cadenas de conexión.  

-   Si usa una llamada OLE DB para iniciar transacciones, hay una diferencia de comportamiento entre el controlador OLE DB para SQL Server y MDAC; las transacciones se iniciarán inmediatamente con el controlador de OLE DB para SQL Server, pero las transacciones se iniciarán después de la primera base de datos tener acceso utilizando MDAC. Esto puede afectar al comportamiento de los procedimientos almacenados y los lotes porque [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] exige que @@TRANCOUNT sea igual una vez que finaliza la ejecución de un procedimiento almacenado o un lote que cuando se inició el lote o el procedimiento almacenado.  

-   Con el controlador OLE DB para SQL Server, ITransactionLocal::BeginTransaction hará que una transacción se inicie inmediatamente. Con MDAC, el inicio de una transacción se retrasa hasta que la aplicación ejecuta una instrucción que requiere una transacción en modo de transacción implícita. Para obtener más información, vea [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../../t-sql/statements/set-implicit-transactions-transact-sql.md).  


 Ambos controlador OLE DB para SQL Server como MDAC admiten leer con las versiones de fila, pero solo controlador de OLE DB para el aislamiento de transacción de instantánea de SQL Server admite el aislamiento de transacción confirmada. (En términos de programación, el aislamiento de transacción de lectura confirmada con versiones de fila es igual que la transacción de lectura confirmada.)  

## <a name="see-also"></a>Ver también  
 [Compilación de aplicaciones con el controlador OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
