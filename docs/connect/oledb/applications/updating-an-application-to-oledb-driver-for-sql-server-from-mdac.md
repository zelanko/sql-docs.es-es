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
ms.openlocfilehash: ad36a17367b14a48810d83137b2887eaa75f6ef1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989261"
---
# <a name="updating-an-application-to-ole-db-driver-for-sql-server-from-mdac"></a>Actualización de una aplicación al controlador OLE DB para SQL Server desde MDAC
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Existen varias diferencias entre el controlador OLE DB para SQL Server y Componentes de Microsoft Data Access (MDAC); a partir de Windows Vista, los componentes de acceso a datos se denominan Componentes de Windows Data Access (o Windows DAC). Aunque ambos proporcionan acceso de datos nativo a las bases de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], el controlador OLE DB para SQL Server se ha diseñado para exponer las nuevas características de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y, al mismo tiempo, mantener la compatibilidad con versiones anteriores.   

 Además, aunque MDAC contiene componentes para usar OLE DB, ODBC y Objetos de datos ActiveX (ADO), OLE DB driver for SQL Server solo implementa OLE DB (aunque ADO puede tener acceso a la funcionalidad de OLE DB controlador para SQL Server).  

 OLE DB controlador para SQL Server y MDAC difieren en las otras áreas siguientes:  

-   Los usuarios que usan ADO para tener acceso al controlador de OLE DB para SQL Server pueden encontrar menos funcionalidad de filtrado que cuando tienen acceso al proveedor de OLE DB de SQL.  

-   Si una aplicación ADO utiliza OLE DB controlador para SQL Server e intenta actualizar una columna calculada, se generará un error. Con MDAC, la actualización se acepta, pero se omite.  

-   OLE DB controlador de SQL Server es un único archivo de biblioteca de vínculos dinámicos (DLL) independiente. Las interfaces que se exponen públicamente se han reducido al mínimo, tanto para facilitar la distribución como para limitar la exposición a riesgos de seguridad.  

-   Solo se admiten interfaces OLE DB.  

-   El controlador de OLE DB para los nombres de SQL Server es diferente de los nombres que se usan con MDAC.  

-   La funcionalidad accesible para el usuario proporcionada por los componentes de MDAC está disponible cuando se usa OLE DB driver for SQL Server. Entre otras características, se incluyen las siguientes: agrupación de conexiones, compatibilidad con ADO y compatibilidad con cursores de cliente. Cuando se usa cualquiera de estas características, OLE DB controlador para SQL Server solo proporciona conectividad de base de datos. MDAC proporciona funciones como seguimiento, controles de administración y contadores de rendimiento.  

-   Las aplicaciones pueden usar los servicios principales de OLE DB con el controlador OLE DB para SQL Server, pero si se usa el motor de cursores de OLE DB, deben usar la opción de compatibilidad de tipo de datos para evitar cualquier problema que pudiera surgir debido al desconocimiento de los nuevos tipos de datos de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] por parte del motor de cursores.  

-   OLE DB controlador para SQL Server admite el acceso a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] bases de datos anteriores.  

-   OLE DB controlador para SQL Server no contiene integración con XML. OLE DB controlador para SQL Server admite SELECT... Consultas FOR XML, pero no admite ninguna otra funcionalidad XML. Sin embargo, OLE DB controlador para SQL Server admite el tipo de datos **XML** introducido [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]en.  

-   El controlador OLE DB para SQL Server admite la configuración de bibliotecas de red de cliente mediante atributos de cadena de conexión solamente. Si necesita una configuración de biblioteca de red más completa, debe usar el Administrador de configuración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  

-   Las cadenas de conexión de MDAC permiten un valor booleano (**true**) para la palabra clave **Trusted_Connection** . Un controlador de OLE DB para la cadena de conexión de SQL Server debe utilizar **sí** o **no**.  

-   Se han realizado pequeños cambios en los errores y advertencias. Ahora, los errores y las advertencias que devuelve el servidor conservan la misma gravedad cuando se pasan al controlador OLE DB para SQL Server. Debe asegurarse de que ha probado de forma exhaustiva la aplicación si depende de la interceptación de determinados errores y advertencias.  

-   El controlador OLE DB para SQL Server dispone de un sistema de comprobación de errores más estricto que MDAC, lo que significa que algunas aplicaciones que no se ajustan estrictamente a las especificaciones de OLE DB pueden comportarse de manera diferente. Por ejemplo, el proveedor SQLOLEDB no exigía la regla consistente en que los nombres de parámetro deben comenzar por "\@" para los parámetros de resultado, pero el controlador OLE DB de SQL Server sí.  

-   OLE DB controlador de SQL Server se comporta de forma diferente a MDAC con respecto a las conexiones con error. Por ejemplo, MDAC devuelve valores de propiedad almacenados en caché para una conexión con errores, mientras que el controlador OLE DB para SQL Server notifica un error a la aplicación que realiza la llamada.  

-   El controlador OLE DB para SQL Server no genera eventos de Visual Studio Analyzer, sino eventos de seguimiento de Windows.  

-   No se puede usar OLE DB controlador para SQL Server con Perfmon. Perfmon es una herramienta de Windows que solo puede utilizarse con los DSN que usan el controlador MDAC SQLODBC que se incluye con Windows.  

-   Cuando OLE DB controlador para SQL Server está conectado a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y versiones posteriores, el error de servidor 16947 se devuelve como SQL_ERROR. Este error se produce cuando una actualización o eliminación posicionada genera errores al actualizar o eliminar una fila. Con MDAC al conectarse a cualquier versión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], se devuelve el error de servidor 16947 como una advertencia (SQL_SUCCESS_WITH_INFO).  

-   El controlador OLE DB para SQL Server implementa la interfaz **IDBDataSourceAdmin**, que es una interfaz opcional de OLE DB que no se implementaba anteriormente, aunque solo se implementa el método **CreateDataSource** de esta interfaz opcional. [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  

-   El controlador OLE DB para SQL Server devuelve sinónimos en los conjuntos de filas de esquema TABLES y TABLE_INFO, con TABLE_TYPE establecido en SYNONYM.  

-   Los valores devueltos de tipo de datos **varchar(max)** , **nvarchar(max)** , **varbinary(max)** , **xml**, **udt** u otros tipos de objetos grandes no pueden devolverse a versiones de cliente anteriores a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Si desea utilizar estos tipos como valores devueltos, debe usar OLE DB controlador para SQL Server.  

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

     Esta asignación de tipos afecta a los valores devueltos para los metadatos de columna. Por ejemplo, una columna de **texto** tiene un tamaño máximo de 2.147.483.647, pero OLE DB controlador de SQL Server informa del tamaño máximo de las columnas **VARCHAR (max)** como 2.147.483.647 o-1, dependiendo de la plataforma.  

-   El controlador OLE DB para SQL Server permite la ambigüedad en las cadenas de conexión por motivos de compatibilidad con versiones anteriores (por ejemplo, algunas palabras clave pueden especificarse más de una vez y pueden permitirse palabras clave en conflicto cuya resolución se base en la posición o en la precedencia). Es posible que las versiones futuras de OLE DB controlador para SQL Server no permitan la ambigüedad en las cadenas de conexión. Al modificar aplicaciones, es recomendable usar el controlador OLE DB para SQL Server a fin de eliminar cualquier dependencia sobre la ambigüedad de las cadenas de conexión.  

-   Si usa una llamada OLE DB para iniciar transacciones, hay una diferencia en el comportamiento entre OLE DB controlador para SQL Server y MDAC; las transacciones se iniciarán inmediatamente con OLE DB controlador para SQL Server, pero las transacciones se iniciarán después del primer acceso a la base de datos mediante MDAC. Esto puede afectar al comportamiento de los procedimientos almacenados y los lotes porque [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] exige que @@TRANCOUNT sea igual una vez que finaliza la ejecución de un procedimiento almacenado o un lote que cuando se inició el lote o el procedimiento almacenado.  

-   Con OLE DB controlador para SQL Server, ITransactionLocal:: BeginTransaction hará que una transacción se inicie de inmediato. Con MDAC, el inicio de una transacción se retrasa hasta que la aplicación ejecuta una instrucción que requiere una transacción en modo de transacción implícita. Para obtener más información, vea [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../../t-sql/statements/set-implicit-transactions-transact-sql.md).  


 Tanto el controlador de OLE DB para SQL Server como MDAC admiten el aislamiento de transacción de lectura confirmada mediante las versiones de fila, pero solo OLE DB controlador para SQL Server admite el aislamiento de transacciones de instantáneas. (En términos de programación, el aislamiento de transacción de lectura confirmada con versiones de fila es igual que la transacción de lectura confirmada.)  

## <a name="see-also"></a>Consulte también  
 [Compilación de aplicaciones con el controlador OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
