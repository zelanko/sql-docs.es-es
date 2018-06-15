---
title: Actualizar una aplicación a controlador OLE DB para SQL Server de MDAC | Documentos de Microsoft
description: Actualizar una aplicación a controlador de OLE DB para SQL Server de MDAC
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
ms.openlocfilehash: 11597ed3b7cd80cae8604291bd8b662bf6a9ed80
ms.sourcegitcommit: 354ed9c8fac7014adb0d752518a91d8c86cdce81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/14/2018
ms.locfileid: "35612110"
---
# <a name="updating-an-application-to-ole-db-driver-for-sql-server-from-mdac"></a>Actualizar una aplicación a controlador OLE DB para SQL Server de MDAC
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Hay una serie de diferencias entre el controlador OLE DB para SQL Server y Microsoft Data Access Components (MDAC); a partir de Windows Vista, los componentes de acceso a datos se denominan ahora Windows Data Access Components (o Windows DAC). Aunque ambos proporcionan acceso a datos nativos a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] bases de datos, controlador de OLE DB para SQL Server se ha diseñado para exponer las nuevas características de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], al mismo tiempo, mantener la compatibilidad con versiones anteriores.   

 Además, aunque MDAC contiene componentes para el uso de OLE DB, ODBC y ActiveX Data Objects (ADO), controlador de OLE DB para SQL Server solo implementa OLE DB (aunque ADO puede tener acceso a la funcionalidad del controlador de OLE DB para SQL Server).  

 Controlador de OLE DB para SQL Server y MDAC difieren en las áreas siguientes:  

-   Los usuarios que utilicen ADO para obtener acceso al controlador de OLE DB para SQL Server pueden encontrar menos funcionalidad de filtrado que cuando tiene acceso el proveedor OLE DB de SQL.  

-   Si una aplicación ADO utiliza el controlador OLE DB para SQL Server y se intenta actualizar una columna calculada, se notificará un error. Con MDAC, la actualización se acepta, pero pasa por alto.  

-   Controlador de OLE DB para SQL Server es un archivo de biblioteca (DLL) de solo vínculo dinámico independiente. Las interfaces que se exponen públicamente se han reducido al mínimo, tanto para facilitar la distribución como para limitar la exposición a riesgos de seguridad.  

-   Se admiten únicamente las interfaces OLE DB.  

-   El controlador OLE DB para los nombres de SQL Server son diferentes de nombres que se usan con MDAC.  

-   Accesibles a los usuarios funcionalidad proporcionada por componentes MDAC está disponible cuando se utiliza el controlador OLE DB para SQL Server. Entre otras características, se incluyen las siguientes: agrupación de conexiones, compatibilidad con ADO y compatibilidad con cursores de cliente. Cuando se utiliza cualquiera de estas características, controlador de OLE DB para SQL Server proporciona sólo la conectividad de bases de datos. MDAC proporciona funciones como seguimiento, controles de administración y contadores de rendimiento.  

-   Aplicaciones pueden usar servicios principales de OLE DB con el controlador OLE DB para SQL Server, pero si usa el motor de cursor de OLE DB, debe usar la opción de compatibilidad de tipo de datos para evitar cualquier problema que pudiera surgir debido a que el motor de cursor no tiene ningún conocimiento del nuevo [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] tipos de datos.  

-   Controlador de OLE DB para SQL Server admite el acceso a la anterior [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] bases de datos.  

-   Controlador de OLE DB para SQL Server no contiene integración de XML. Controlador de OLE DB para SQL Server admite SELECT... PARA las consultas XML, pero no admite ninguna otra funcionalidad XML. Sin embargo, controlador de OLE DB para SQL Server es compatible con la **xml** tipo de datos que se introdujo en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  

-   Controlador de OLE DB para SQL Server admite la configuración de bibliotecas de red del lado cliente con solo los atributos de cadena de conexión. Si necesita una configuración de biblioteca de red más completa, debe usar el Administrador de configuración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  

-   Las cadenas de conexión de MDAC permiten un valor booleano (**true**) para la **Trusted_Connection** palabra clave. Debe usar un controlador de OLE DB para la cadena de conexión de SQL Server **Sí** o **sin**.  

-   Se han realizado pequeños cambios en los errores y advertencias. Las advertencias y errores devueltos por el servidor ahora conservan la misma gravedad cuando se pasa al controlador de OLE DB para SQL Server. Debe asegurarse de que ha probado de forma exhaustiva la aplicación si depende de la interceptación de determinados errores y advertencias.  

-   Controlador de OLE DB para SQL Server tiene más estricta error al comprobar que MDAC, lo que significa que algunas aplicaciones que no se ajustan estrictamente a las especificaciones de OLE DB pueden comportarse de manera diferente. Por ejemplo, el proveedor SQLOLEDB no forzó la regla que los nombres de parámetro deben comenzar con ' @' para resultados de parámetros, pero el controlador OLE DB para SQL Server lleva a cabo.  

-   Controlador OLE DB para SQL Server se comportan de forma diferente a MDAC con respecto a los errores de conexión. Por ejemplo, MDAC devuelve valores de propiedad almacenados en caché para una conexión que ha dado error, mientras que el controlador OLE DB para SQL Server informa de un error a la aplicación que realiza la llamada.  

-   Controlador de OLE DB para SQL Server no genera eventos de Visual Studio Analyzer, sino que genera eventos de seguimiento de Windows.  

-   No se puede usar el controlador OLE DB para SQL Server con perfmon. Perfmon es una herramienta de Windows que solo puede utilizarse con los DSN que usan el controlador MDAC SQLODBC que se incluye con Windows.  

-   Cuando está conectado el controlador OLE DB para SQL Server a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y versiones posteriores, el error de servidor 16947 se devuelve como SQL_ERROR. Este error se produce cuando una actualización o eliminación posicionada genera errores al actualizar o eliminar una fila. Con MDAC al conectarse a cualquier versión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], se devuelve el error de servidor 16947 como una advertencia (SQL_SUCCESS_WITH_INFO).  

-   Controlador de OLE DB para SQL Server implementa la **IDBDataSourceAdmin** interfaz, que es una interfaz OLE DB opcional que no se implementaba previamente, pero solo el **CreateDataSource** método de este se implementa la interfaz opcional. [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  

-   El controlador OLE DB para SQL Server devuelve sinónimos en las tablas y TABLE_INFO conjuntos de filas de esquema, con TABLE_TYPE establecido en SYNONYM.  

-   Valores devueltos de tipo de datos **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **xml**, **udt**, o de otros tipos de objetos grandes no se puede devolver al cliente de versiones anteriores a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Si desea usar estos tipos como valores devueltos, debe usar el controlador OLE DB para SQL Server.  

-   MDAC permite las siguientes instrucciones que se ejecutará en el inicio de transacciones manuales e implícitas, pero no es el controlador OLE DB para SQL Server. Deben ejecutarse en modo de confirmación automática.  

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

-   Controlador de OLE DB para SQL Server permite la ambigüedad en las cadenas de conexión (por ejemplo, algunas palabras clave se puede especificar más de una vez y puede permitirse palabras clave en conflicto cuya resolución se base en la posición o precedencia) por motivos de compatibilidad con versiones anteriores. Las versiones futuras del controlador de OLE DB para SQL Server quizás no permitan ambigüedad en las cadenas de conexión. Es recomendable para modificar las aplicaciones para usar el controlador OLE DB para SQL Server para eliminar cualquier dependencia de ambigüedad de la cadena de conexión.  

-   Si usa una llamada OLE DB para iniciar las transacciones, hay una diferencia de comportamiento entre el controlador OLE DB para SQL Server y MDAC; las transacciones se iniciarán inmediatamente con el controlador OLE DB para SQL Server, pero las transacciones se iniciarán después de la primera base de datos tener acceso utilizando MDAC. Esto puede afectar al comportamiento de los procedimientos almacenados y lotes porque [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] requiere@TRANCOUNT sean las mismas cuando un lote o procedimiento almacenado finaliza la ejecución tal como estaba al inicia el procedimiento almacenado o lote.  

-   Con el controlador OLE DB para SQL Server, ITransactionLocal::BeginTransaction hará que una transacción se inicie inmediatamente. Con MDAC el inicio de transacciones se retrasa hasta que la aplicación ejecuta una instrucción que requiere una transacción en modo de transacción implícita. Para obtener más información, vea [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../../t-sql/statements/set-implicit-transactions-transact-sql.md).  


 Ambos controlador OLE DB para SQL Server como MDAC admiten el aislamiento de transacción confirmada mediante las versiones de fila, pero sólo controlador OLE DB para el aislamiento de transacción de instantánea de SQL Server admite de lectura. (En términos de programación, el aislamiento de transacción de lectura confirmada con versiones de fila es igual que la transacción de lectura confirmada.)  

## <a name="see-also"></a>Vea también  
 [Compilación de aplicaciones con el controlador OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
