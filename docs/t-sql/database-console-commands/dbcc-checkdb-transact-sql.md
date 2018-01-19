---
title: DBCC CHECKDB (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 12/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHECKDB_TSQL
- DBCC_CHECKDB_TSQL
- DBCC CHECKDB
- CHECKDB
dev_langs: TSQL
helpviewer_keywords:
- CHECKDB [DBCC statement]
- database objects [SQL Server], checking
- counting pages
- per-index row counts
- per-table row counts
- DBCC CHECKDB statement
- per-table page counts
- allocation checks
- integrity [SQL Server], database objects
- per-index page counts
- counting rows
- table integrity checks [SQL Server]
- row count accuracy [SQL Server]
- negative counts
- checking database objects
- page count accuracy [SQL Server]
ms.assetid: 2c506167-0b69-49f7-9282-241e411910df
caps.latest.revision: "144"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 49cf7311995d2760306e6050e6bae6efc1db41d8
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/19/2018
---
# <a name="dbcc-checkdb-transact-sql"></a>DBCC CHECKDB (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Comprueba la integridad física y lógica de todos los objetos de la base de datos especificada mediante la realización de las siguientes operaciones:    
    
-   Se ejecuta [DBCC CHECKALLOC](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md) en la base de datos.    
-   Se ejecuta [DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md) en cada tabla y vista en la base de datos.    
-   Se ejecuta [DBCC CHECKCATALOG](../../t-sql/database-console-commands/dbcc-checkcatalog-transact-sql.md) en la base de datos.    
-   Valida el contenido de cada vista indizada de la base de datos.    
-   Valida la coherencia de nivel de vínculo entre los archivos y directorios del sistema de archivos y metadatos de tabla al almacenar **varbinary (max)** datos del sistema de archivos con FILESTREAM.    
-   Valida los datos de [!INCLUDE[ssSB](../../includes/sssb-md.md)] en la base de datos.    
    
Esto significa que los comandos DBCC CHECKALLOC, DBCC CHECKTABLE o DBCC CHECKCATALOG no tienen que ejecutarse por separado de DBCC CHECKDB. Para obtener información más detallada sobre las comprobaciones que realizan estos comandos, vea sus descripciones.    
 
> [!NOTE]
> DBCC CHECKDB se admite en bases de datos que contienen tablas optimizadas para memoria, pero la validación solo se produce en tablas basadas en disco. Sin embargo, como parte de la copia de seguridad y la recuperación de bases de datos, la validación de CHECKSUM se realiza para los archivos de grupos de archivos optimizados para memoria.    
>     
> Puesto que las opciones de reparación de DBCC no están disponibles para las tablas optimizadas para memoria, debe hacer periódicamente copia de seguridad de las bases de datos y probar dichas copias. Si se producen problemas de integridad de datos en una tabla optimizada para memoria, debe restaurar desde la última copia de seguridad válida conocida.    

![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>Sintaxis    
    
```    
DBCC CHECKDB     
    [ ( database_name | database_id | 0    
        [ , NOINDEX     
        | , { REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD } ]    
    ) ]    
    [ WITH     
        {    
            [ ALL_ERRORMSGS ]    
            [ , EXTENDED_LOGICAL_CHECKS ]     
            [ , NO_INFOMSGS ]    
            [ , TABLOCK ]    
            [ , ESTIMATEONLY ]    
            [ , { PHYSICAL_ONLY | DATA_PURITY } ]    
            [ , MAXDOP  = number_of_processors ]    
        }    
    ]    
]    
```    
    
## <a name="arguments"></a>Argumentos    
 *database_name* | *database_id* | 0  
 Es el nombre o Id. de la base de datos para la que se van a ejecutar comprobaciones de integridad. Si no se especifica o se especifica 0, se utiliza la base de datos actual. Nombres de base de datos deben cumplir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md).  
    
NOINDEX  
 Especifica que no se deben realizar comprobaciones intensivas de índices no clúster para las tablas de usuario. Esto reduce el tiempo total de ejecución. NOINDEX no afecta a las tablas del sistema, porque las comprobaciones de integridad siempre se realizan en los índices de las tablas del sistema.  
    
REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD  
 Especifica que DBCC CHECKDB repare los errores que encuentre. Utilice las opciones REPAIR solo como último recurso. La base de datos especificada debe estar en modo de usuario único para utilizar una de las siguientes opciones de reparación.  
    
REPAIR_ALLOW_DATA_LOSS  
 Intenta reparar todos los errores indicados. Estas reparaciones pueden ocasionar alguna pérdida de datos.  
    
> [!WARNING]
> La opción REPAIR_ALLOW_DATA_LOSS es una característica compatible pero no siempre es la mejor opción para poner una base de datos a un estado físicamente coherente. Si se realiza correctamente, la opción REPAIR_ALLOW_DATA_LOSS puede provocar la pérdida de datos. De hecho, puede producir la pérdida de más datos que si un usuario tuviera que restaurar la base de datos desde la última copia de seguridad en buen estado. 
>
> En [!INCLUDE[msCoName](../../includes/msconame-md.md)] siempre se recomienda que el usuario haga una restauración de la última copia de seguridad correcta como método principal para corregir los errores notificados por DBCC CHECKDB. La opción REPAIR_ALLOW_DATA_LOSS no es una alternativa para restaurar a partir de una copia de seguridad buena. Es una opción de emergencia como "último recurso" que solo se recomienda utilizar si no es posible restaurar a partir de una copia de seguridad.    
>     
> Algunos errores, que solamente pueden repararse mediante la opción REPAIR_ALLOW_DATA_LOSS, pueden implicar desasignar una fila, una página o una serie de páginas para borrar los errores. El usuario ya no puede acceder a los datos desasignados ni puede recuperarlos, y no se puede determinar el contenido exacto de los datos desasignados. Por lo tanto, puede ser que la integridad referencial no sea precisa tras desasignar filas o páginas porque la comprobación  y el mantenimiento de las restricciones de la clave externa no forman parte de esta operación de reparación. El usuario debe inspeccionar la integridad referencial de su base de datos (DBCC CHECKCONSTRAINTS) después de usar la opción REPAIR_ALLOW_DATA_LOSS.    
>     
> Antes de realizar la reparación, cree copias físicas de los archivos que pertenezcan a esta base de datos. Esto incluye el archivo de datos principal (.mdf), los archivos de datos secundarios (.ndf), todos los archivos de registro de transacciones (.ldf) y otros contenedores que forman la base de datos como catálogos de texto completo, carpetas de secuencia de archivos, datos optimizados en memoria, etc.    
>     
> Antes de realizar la reparación, plantéese cambiar el estado de la base de datos al modo EMERGENCY, intente extraer tanta información como sea posible de las tablas críticas y guarde esos datos.    
    
REPAIR_FAST  
 La sintaxis se mantiene únicamente por compatibilidad con versiones anteriores. No se realizan acciones de reparación.  
    
REPAIR_REBUILD  
 Realiza reparaciones que no tienen ninguna posibilidad de pérdida de datos. Pueden ser reparaciones rápidas, como la reparación de las filas que faltan en índices no clúster, y reparaciones que consumen más tiempo, como regenerar un índice.  
 Este argumento no repara los errores que implican datos de FILESTREAM.  
    
> [!IMPORTANT] 
> Puesto que se puede registrar y recuperar completamente DBCC CHECKDB junto con cualquiera de las opciones de REPAIR, en [!INCLUDE[msCoName](../../includes/msconame-md.md)] siempre se recomienda que el usuario utilice CHECKDB con las opciones de REPAIR dentro de una transacción (ejecute BEGIN TRANSACTION antes de ejecutar el comando) para que el usuario pueda confirmar si quiere aceptar los resultados de la operación. A continuación, el usuario puede ejecutar COMMIT TRANSACTION para confirmar todo el trabajo realizado por la operación de reparación. Si el usuario no desea aceptar el resultado de la operación, puede ejecutar ROLLBACK TRANSACTION para deshacer los efectos de las operaciones de reparación.    
>     
> Para reparar errores, se recomienda restaurar a partir de una copia de seguridad. Las operaciones de reparación no tienen en cuenta ninguna de las restricciones que puede haber en las tablas o entre ellas. Si la tabla especificada está implicada en una o más restricciones, se recomienda ejecutar DBCC CHECKCONSTRAINTS tras una operación de reparación. Si debe utilizar REPAIR, ejecute DBCC CHECKDB sin una opción de reparación para localizar el nivel de reparación que se va a utilizar. Si utiliza el nivel REPAIR_ALLOW_DATA_LOSS, se recomienda realizar una copia de seguridad de la base de datos antes de ejecutar DBCC CHECKDB con esta opción.    
    
ALL_ERRORMSGS  
 Muestra todos los errores notificados por objeto. De forma predeterminada, se muestran todos los mensajes de error. Especificar u omitir esta opción no tiene ningún efecto. Mensajes de error se ordenan por identificador de objeto, excepto para los mensajes generados desde [base de datos tempdb](../../relational-databases/databases/tempdb-database.md).     

EXTENDED_LOGICAL_CHECKS  
 Si el nivel de compatibilidad es 100 ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]) o superior, realiza comprobaciones de coherencia lógica en una vista indizada, en índices XML y en índices espaciales, en caso de que los haya.  
 Para obtener más información, consulte *realizar comprobaciones lógicas de coherencia en índices*, en la [comentarios](#remarks) sección más adelante en este tema.  
    
NO_INFOMSGS  
 Suprime todos los mensajes de información.  
    
TABLOCK  
 Hace que DBCC CHECKDB obtenga bloqueos en lugar de utilizar una instantánea de base de datos interna. Se incluye un bloqueo exclusivo (X) a corto plazo en la base de datos. TABLOCK hace que DBCC CHECKDB se ejecute más rápido en una base de datos con mucha carga, pero disminuye la simultaneidad disponible en la base de datos mientras DBCC CHECKDB está en ejecución.  
    
> [!IMPORTANT] 
> TABLOCK limita las comprobaciones que se llevan a cabo; DBCC CHECKCATALOG no se ejecuta en la base de datos y los datos de [!INCLUDE[ssSB](../../includes/sssb-md.md)] no se validan.
    
ESTIMATEONLY  
 Muestra la cantidad estimada de espacio de tempdb que se requiere para ejecutar DBCC CHECKDB con todas las demás opciones especificadas. No se realiza la comprobación real de la base de datos.  
    
PHYSICAL_ONLY  
 Limita la comprobación a la integridad de la estructura física de los encabezados de página y registro y la coherencia de la asignación de la base de datos. Esta comprobación se ha diseñado para proporcionar una pequeña comprobación de sobrecarga de la coherencia física de la base de datos; también detecta páginas rasgadas, errores de suma de comprobación y errores de hardware comunes que pueden comprometer los datos del usuario.  
 La ejecución completa de DBCC CHECKDB puede tardar mucho más tiempo en completarse que en versiones anteriores. Este comportamiento se produce porque:  
 -   Las comprobaciones lógicas son más exhaustivas.  
 -   Algunas de las estructuras subyacentes que hay que comprobar son más complejas.  
 -   Se han agregado muchas comprobaciones nuevas para incluir las nuevas características.  
 Por lo tanto, el uso de la opción PHYSICAL_ONLY puede llevar mucho menos tiempo para DBCC CHECKDB en bases de datos grandes y es por esa razón por la que se recomienda para un uso frecuente en sistemas de producción. Aun así, se recomienda realizar periódicamente una ejecución completa DBCC CHECKDB. La frecuencia de estas ejecuciones depende de factores específicos de cada empresa y de los entornos de producción.    
Este argment siempre implica NO_INFOMSGS y no se permite con cualquiera de las opciones de reparación.  
    
> [!WARNING] 
> Si se especifica PHYSICAL_ONLY, DBCC CHECKDB omite todas las comprobaciones de datos de FILESTREAM.
    
DATA_PURITY  
 Hace que DBCC CHECKDB compruebe si la base de datos contiene valores de columna que no son válidos o están fuera del intervalo correcto. Por ejemplo, DBCC CHECKDB detecta las columnas con valores de fecha y hora son superiores o inferiores el intervalo para la **datetime** tipo de datos; o **decimal** o tipo de datos numérico aproximado columnas con valores de escala o precisión que no son válidos.  
 Las comprobaciones de integridad de valores de columna están habilitadas de manera predeterminada y no requieren la opción DATA_PURITY. De manera predeterminada, en las bases de datos actualizadas desde versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], las comprobaciones de valores de columna no se habilitan hasta que no se ejecuta DBCC CHECKDB WITH DATA_PURITY sin errores en la base de datos. Después, DBCC CHECKDB comprueba la integridad de los valores de columna de manera predeterminada. Para obtener más información sobre cómo podría afectar a CHECKDB la actualización de bases de datos de versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea la sección Comentarios más adelante en este tema.  
    
> [!WARNING]
> Si se especifica PHYSICAL_ONLY, no se realizan comprobaciones de integridad de columna.
    
 Los errores de validación de los que informe esta opción no se pueden corregir con las opciones de reparación de DBCC. Para obtener información acerca de cómo corregir manualmente estos errores, vea el artículo 923247 de Knowledge Base: [solucionar el error DBCC 2570 en SQL Server 2005 y versiones posteriores](http://support.microsoft.com/kb/923247).  
    
 MAXDOP  
 **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
    
 Invalida el **grado máximo de paralelismo** opción de configuración de **sp_configure** para la instrucción. El MAXDOP puede superar el valor configurado con sp_configure. Si MAXDOP supera el valor configurado con el regulador de recursos, el [!INCLUDE[ssDEnoversion](../../includes/ssDEnoversion_md.md)] utiliza el valor de MAXDOP del regulador de recursos, se describe en [ALTER WORKLOAD GROUP](../../t-sql/statements/alter-workload-group-transact-sql.md). Se pueden aplicar todas las reglas semánticas utilizadas con la opción de configuración max degree of parallelism cuando se utiliza la sugerencia de consulta MAXDOP. Para obtener más información, vea [Establecer la opción de configuración del servidor Grado máximo de paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).  
 
> [!WARNING] 
> Si MAXDOP se establece en cero, a continuación, SQL Server elige el grado máximo de paralelismo para usar.    

## <a name="remarks"></a>Comentarios    
DBCC CHECKDB no examina los índices deshabilitados. Para obtener más información acerca de los índices deshabilitados, vea [deshabilitar índices y restricciones](../../relational-databases/indexes/disable-indexes-and-constraints.md).    

Si un tipo definido por el usuario se marca como ordenado por bytes, solo debe existir una serialización del tipo definido por el usuario. La serialización incoherente de los tipos definidos por el usuario ordenados por bytes provoca el error 2537 cuando se ejecuta DBCC CHECKDB. Para obtener más información, consulte [requisitos de tipo definido por el usuario](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-requirements.md).    

Dado que la [base de datos de recursos](../../relational-databases/databases/resource-database.md) es modificable sólo en modo de usuario único, DBCC CHECKDB comando no se puede ejecutar directamente en ella. Sin embargo, cuando se ejecuta DBCC CHECKDB en la [base de datos maestra](../../relational-databases/databases/master-database.md), también se ejecuta un segundo comando CHECKDB internamente en la base de datos de recursos. Esto significa que DBCC CHECKDB puede devolver resultados adicionales. El comando devuelve conjuntos de resultados adicionales cuando no se establecen opciones o cuando se establecen las opciones PHYSICAL_ONLY o ESTIMATEONLY.    

A partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP2, ejecutar DBCC CHECKDB **ya no** borra la caché del plan para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Antes de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP2, ejecutar DBCC CHECKDB borra la caché del plan. Al borrar la caché del plan, se provoca una recompilación de todos los planes de ejecución posteriores y puede ocasionar una disminución repentina y temporal del rendimiento de las consultas. 
    
## <a name="performing-logical-consistency-checks-on-indexes"></a>Realizar comprobaciones de coherencia lógica en índices    
La comprobación de coherencia lógica en índices varía según el nivel de compatibilidad de la base de datos, tal como se indica a continuación:
-   Si el nivel de compatibilidad es 100 ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]) o superior:    
-   A menos que se especifique NOINDEX, DBCC CHECKDB realiza comprobaciones de coherencia física y lógica en una sola tabla y en todos sus índices no clúster. Sin embargo, en los índices XML, índices espaciales y vistas indizadas solo se realizan comprobaciones de coherencia física de forma predeterminada.
-   Si se especifica WITH EXTENDED_LOGICAL_CHECKS, se realizarán comprobaciones lógicas en una vista indizada, en índices XML e índices espaciales, en caso de que los hubiese. De forma predeterminada, las comprobaciones de coherencia física se realizan antes que las comprobaciones de coherencia lógica. Si también se especifica NOINDEX, solamente se realizarán las comprobaciones lógicas.
    
Estas comprobaciones de coherencia lógica realizan una comprobación cruzada de la tabla de índices interna del objeto de índice con la tabla de usuario a la que hace referencia. Para buscar las filas periféricas, se crea una consulta interna que lleve a cabo una intersección completa de las tablas internas y del usuario. La ejecución de esta consulta puede afectar mucho al rendimiento y no se puede realizar el seguimiento de su progreso. Por consiguiente, se recomienda especificar únicamente WITH EXTENDED_LOGICAL_CHECKS si cree que existen problemas del índice que no estén relacionados con daños físicos, o si las sumas de comprobación del nivel de página se han desactivado y sospecha que puedan existir daños de hardware de nivel de columna.
-   Si el índice es un índice filtrado, DBCC CHECKDB realizará las comprobaciones de coherencia para comprobar que las entradas de índice satisfacen el predicado de filtro.
-   Si el nivel de compatibilidad es 90 o menos, a menos que se especifique NOINDEX, DBCC CHECKDB realiza las comprobaciones de coherencia física y lógica en una tabla única o vista indizada y en todos sus índices XML e índices no clúster. Los índices espaciales no se admiten.  
- A partir de SQL Server 2016, comprobaciones adicionales en las columnas calculadas persistentes, las columnas UDT y los índices filtrados no se ejecutarán de forma predeterminada para evitar las evaluaciones de expresiones costoso. Este cambio reduce en gran medida el tiempo que dure CHECKDB en bases de datos que contiene estos objetos. Sin embargo, las comprobaciones de coherencia física de estos objetos siempre se completa. Cuando se especifica la opción de EXTENDED_LOGICAL_CHECKS las evaluaciones de expresiones se realizará además de las comprobaciones lógicas ya está presentes (vista indizada, índices XML e índices espaciales) como parte de la opción EXTENDED_LOGICAL_CHECKS.   
    
**Para obtener información sobre el nivel de compatibilidad de una base de datos**
-   [Ver o cambiar el nivel de compatibilidad de una base de datos](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)    
    
## <a name="internal-database-snapshot"></a>Instantánea de base de datos interna    
DBCC CHECKDB utiliza una instantánea interna de la base de datos para la coherencia transaccional necesaria para realizar estas comprobaciones. Así se evitan problemas de bloqueo y simultaneidad cuando se ejecutan estos comandos. Para obtener más información, vea [ver el tamaño del archivo disperso de una instantánea de base de datos &#40; Transact-SQL &#41; ](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md) y la sección uso de instantáneas de base de datos interna DBCC en [DBCC &#40; Transact-SQL &#41; ](../../t-sql/database-console-commands/dbcc-transact-sql.md). Si no se puede crear una instantánea o se especifica TABLOCK, DBCC CHECKDB adquiere bloqueos para obtener la coherencia necesaria. En este caso, se requiere un bloqueo exclusivo de base de datos para realizar las comprobaciones de asignación y se requieren bloqueos compartidos de tabla para realizar las comprobaciones de tabla.
DBCC CHECKDB produce un error cuando se ejecuta en master si no se puede crear una instantánea de base de datos interna.
Ejecutar DBCC CHECKDB en tempdb no realiza ninguna comprobación de asignación ni de catálogos y debe adquirir bloqueos de tabla compartidos para llevar a cabo comprobaciones de la tabla. Esto es debido a que, por motivos de rendimiento, las instantáneas de base de datos no están disponibles en tempdb. Eso significa que no es posible obtener la coherencia transaccional necesaria.
En Microsoft SQL Server 2012 o una versión anterior de SQL Server, puede encontrar mensajes de error al ejecutar el comando DBCC CHECKDB para una base de datos que tenga los archivos ubicados en un volumen con formato ReFS. Para obtener más información, vea el artículo de Knowledge Base 2974455: [comportamiento de DBCC CHECKDB cuando la base de datos de SQL Server se encuentra en un volumen ReFS.](https://support.microsoft.com/kb/2974455)    
    
## <a name="checking-and-repairing-filestream-data"></a>Comprobar y reparar datos de FILESTREAM    
Cuando se habilita FILESTREAM para una base de datos y una tabla, puede almacenar opcionalmente **varbinary (max)** objetos binarios grandes (BLOB) en el sistema de archivos. Al utilizar DBCC CHECKDB en una base de datos que almacena BLOB en el sistema de archivos, DBCC comprueba la coherencia de nivel de vínculo entre el sistema de archivos y la base de datos.
Por ejemplo, si una tabla contiene una **varbinary (max)** columna que utiliza el atributo FILESTREAM, DBCC CHECKDB comprobará que existe una asignación uno a uno entre los directorios de sistema de archivos y archivos y filas de tablas, columnas y columnas valores. DBCC CHECKDB puede reparar el daño producido si se especifica la opción de REPAIR_ALLOW_DATA_LOSS. Para reparar el daño producido en FILESTREAM, DBCC eliminará las filas de tabla que sean datos del sistema de archivos que faltan.
    
## <a name="best-practices"></a>Procedimientos recomendados    
Se recomienda utilizar la opción PHYSICAL_ONLY si se usa con frecuencia en sistemas de producción. El uso de PHYSICAL_ONLY puede reducir mucho el tiempo de ejecución de DBCC CHECKDB en bases de datos grandes. También se recomienda ejecutar DBCC CHECKDB sin opciones de forma periódica. La frecuencia con que se deben realizar estas ejecuciones varía en función de la empresa y su entorno de producción.
    
## <a name="checking-objects-in-parallel"></a>Comprobar objetos en paralelo    
De forma predeterminada, DBCC CHECKDB realiza comprobaciones paralelas de los objetos. El grado de paralelismo se determina automáticamente mediante el procesador de consultas. El grado máximo de paralelismo se configura igual que las consultas paralelas. Para restringir el número máximo de procesadores disponibles para las comprobaciones DBCC, use [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md). Para obtener más información, vea [Establecer la opción de configuración del servidor Grado máximo de paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). La comprobación del paralelismo se puede deshabilitar utilizando el marcador de seguimiento 2528. Para obtener más información, vea [Marcas de seguimiento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).
    
> [!NOTE]
> Esta característica no está disponible en todas las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, ver coherencia en paralelo, consulte en la sección de facilidad de uso de RDBMS de [características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).    
    
## <a name="understanding-dbcc-error-messages"></a>Descripción de los mensajes de error de DBCC    
Cuando finaliza el comando DBCC CHECKDB, se escribe un mensaje en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si el comando DBCC se ejecuta correctamente, el mensaje lo indica, así como el tiempo de ejecución del comando. Si el comando DBCC se detiene antes de finalizar la comprobación debido a un error, el mensaje indica que el comando se ha cancelado, un valor de estado y el tiempo de ejecución del comando. En la tabla siguiente se muestran y describen los valores de estado que pueden aparecer en el mensaje.
    
|State|Description|    
|-----------|-----------------|    
|0|Se ha generado el error número 8930. Esto indica que se interrumpió la ejecución del comando DBCC a causa de daños en los metadatos.|    
|1|Se ha generado el error número 8967. Error DBCC interno.|    
|2|Error durante una reparación de base de datos en modo de emergencia.|    
|3|Esto indica que se interrumpió la ejecución del comando DBCC a causa de daños en los metadatos.|    
|4|Se ha detectado una infracción de acceso o aserción.|    
|5|Error desconocido que cancela el comando DBCC.|    
    
## <a name="error-reporting"></a>Informes de errores    
Un archivo de volcado (`SQLDUMP*nnnn*.txt`) se crea en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] directorio de registro cada vez que DBCC CHECKDB detecta un error por daños. Cuando el *uso de características* la recopilación de datos y *informe de errores de* características están habilitadas para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el archivo se reenvía automáticamente a [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Los datos recopilados se utilizan para mejorar la funcionalidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
El archivo de volcado contiene los resultados del comando DBCC CHECKDB y los resultados del diagnóstico adicional. Acceso está limitado a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta y los miembros del rol sysadmin de servicio. De forma predeterminada, la función sysadmin contiene todos los miembros de las ventanas `BUILTIN\Administrators` grupo y el grupo de administradores local. El comando DBCC no producirá error en caso de que se produzca un error en el proceso de recopilación de datos.
    
## <a name="resolving-errors"></a>Resolver errores    
Si DBCC CHECKDB informa de errores, se recomienda restaurar la base de datos a partir de una copia de seguridad en lugar de ejecutar REPAIR con una de sus opciones. Si no hay ninguna copia de seguridad, al ejecutar REPAIR se corrigen los errores notificados. La opción de reparación que se debe utilizar se especifica al final de la lista de errores notificados. No obstante, la corrección de errores mediante la opción REPAIR_ALLOW_DATA_LOSS puede requerir eliminar algunas páginas y, por tanto, también algunos datos.    

En algunas circunstancias, es posible que la base de datos contenga valores que no son válidos o que no están comprendidos en el intervalo correcto de acuerdo con el tipo de datos de la columna. DBCC CHECKDB puede detectar valores de columna que no son válidos para todos los tipos de datos de columna. Por tanto, al ejecutar DBCC CHECKDB con la opción DATA_PURITY en bases de datos que se han actualizado desde versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], pueden desvelarse errores de valores de columna que ya existían. Dado que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede reparar estos errores de forma automática, será necesario actualizar el valor de la columna de forma manual. Si CHECKDB detecta un error de este tipo, devuelve una advertencia, el número de error 2570 e información para identificar la fila afectada y corregir el error manualmente.    

La reparación se puede realizar en una transacción de usuario para permitirle revertir los cambios realizados. Si se revierten las reparaciones, la base de datos aún contendrá errores por lo que se debe restaurar a partir de una copia de seguridad. Una vez finalizadas las reparaciones, realice una copia de seguridad de la base de datos.
    
## <a name="resolving-errors-in-database-emergency-mode"></a>Resolver errores en modo de emergencia de base de datos    
Cuando una base de datos se ha establecido en modo de emergencia mediante el uso de la [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) instrucción, DBCC CHECKDB puede realizar algunas reparaciones especiales en la base de datos si se especifica la opción REPAIR_ALLOW_DATA_LOSS. Estas reparaciones pueden permitir que bases de datos que normalmente no se pueden recuperar vuelvan a estar en línea con un estado físicamente coherente. Estas reparaciones solo deben utilizarse como último recurso y solo cuando no se puede restaurar la base de datos a partir de una copia de seguridad. Cuando la base de datos se establece en modo de emergencia, la base de datos está marcada como READ_ONLY, el registro está deshabilitado y acceso está limitado a los miembros del rol fijo de servidor sysadmin.
    
> [!NOTE]
> No se puede ejecutar el comando DBCC CHECKDB en modo de emergencia dentro de una transacción de usuario y revertir la transacción tras la ejecución.    
    
Cuando la base de datos está en modo de emergencia y se ejecuta DBCC CHECKDB con la cláusula REPAIR_ALLOW_DATA_LOSS, se realizan las siguientes acciones:
-   DBCC CHECKDB utiliza páginas marcadas como inaccesibles debido a errores de suma de comprobación o de E/S como si los errores no se hubieran producido. De esta manera aumentan las posibilidades de recuperación de datos de la base de datos.    
-   DBCC CHECKDB intenta recuperar la base de datos utilizando las técnicas habituales de recuperación basadas en el registro.    
-   Si la recuperación de la base de datos no puede realizarse debido a daños en el registro de transacciones, dicho registro de transacciones volverá a generarse. Volver a generar el registro de transacciones puede provocar la pérdida de coherencia transaccional.    
    
> [!WARNING]
> La opción REPAIR_ALLOW_DATA_LOSS es una característica compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No obstante, puede que no siempre sea la mejor opción para llevar una base de datos a un estado físicamente coherente. Si se realiza correctamente, la opción REPAIR_ALLOW_DATA_LOSS puede provocar la pérdida de datos. De hecho, puede producir la pérdida de más datos que si un usuario tuviera que restaurar la base de datos desde la última copia de seguridad en buen estado. En [!INCLUDE[msCoName](../../includes/msconame-md.md)] siempre se recomienda que el usuario haga una restauración de la última copia de seguridad correcta como método principal para corregir los errores notificados por DBCC CHECKDB. La opción REPAIR_ALLOW_DATA_LOSS es **no** alternativa para restaurar a partir de una copia de seguridad buena conocida. Es una opción de emergencia como "último recurso" que solo se recomienda utilizar si no es posible restaurar a partir de una copia de seguridad.    
>     
>  Después de volver a generar el registro, no hay ninguna garantía ACID completa.    
>     
>  Después de volver a generar el registro, DBCC CHECKDB se ejecutará automáticamente, informará de los problemas de coherencia física y los corregirá.    
>     
>  Las restricciones reguladas por la lógica empresarial y por la coherencia de datos lógicos se deben validar manualmente.    
>     
>  El tamaño del registro de transacciones conservará su tamaño predeterminado y debe ajustarse manualmente a su tamaño reciente.    
    
Si el comando DBCC CHECKDB se ejecuta correctamente, la base de datos está en un estado físicamente coherente y se establece su estado en ONLINE. No obstante, la base de datos puede contener una o más incoherencias transaccionales. Le recomendamos que ejecute [DBCC CHECKCONSTRAINTS](../../t-sql/database-console-commands/dbcc-checkconstraints-transact-sql.md) para identificar los errores de lógica de negocios e inmediatamente realizar una copia de la base de datos.
Si el comando DBCC CHECKDB produce un error, no se puede reparar la base de datos.
    
## <a name="running-dbcc-checkdb-with-repairallowdataloss-in-replicated-databases"></a>Ejecutar DBCC CHECKDB con REPAIR_ALLOW_DATA_LOSS en bases de datos replicadas    
La ejecución del comando DBCC CHECKDB con la opción REPAIR_ALLOW_DATA_LOSS puede afectar a las bases de datos de usuario (bases de datos de publicaciones y suscripciones) y a la base de datos de distribución utilizada por la replicación. Las bases de datos de publicaciones y suscripciones incluyen tablas publicadas y tablas de metadatos de replicación. Debe tener en cuenta los siguientes problemas potenciales en estas bases de datos:
-   Tablas publicadas. Puede que no se repliquen las acciones realizadas por el proceso CHECKDB para reparar datos de usuario dañados:    
-   La replicación de mezcla utiliza desencadenadores para realizar el seguimiento de los cambios en tablas publicadas. Si el proceso CHECKDB inserta, actualiza o elimina filas, no se activan los desencadenadores, por lo que el cambio no se replica.
-   La replicación transaccional utiliza el registro de transacciones para realizar el seguimiento de los cambios en tablas publicadas. Posteriormente, el Agente de registro del LOG mueve estos cambios a la base de datos de distribución. Es posible que el Agente de registro del LOG no pueda replicar algunas reparaciones de DBCC, aunque se hayan registrado. Por ejemplo, si el proceso CHECKDB cancela la asignación de una página de datos, el Agente de registro del LOG no convierte esta acción en una instrucción DELETE; por tanto, el cambio no se replica.
-   Tablas de metadatos de replicación. Las acciones que realiza el proceso CHECKDB para reparar tablas de metadatos de replicación dañadas requieren que se quite y se vuelva a configurar la replicación.    
    
Si debe ejecutar el comando DBCC CHECKDB con la opción REPAIR_ALLOW_DATA_LOSS en una base de datos de usuario o en una base de datos de distribución:
1.  Ponga el sistema en modo inactivo: detenga la actividad en la base de datos y en todas las demás bases de datos de la topología de replicación, e intente sincronizar todos los nodos. Para más información, vea [Poner en modo inactivo una topología de replicación &#40;programación de la replicación con Transact-SQL&#41;](../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md).    
1.  Ejecute DBCC CHECKDB.    
1.  Si el informe de DBCC CHECKDB incluye reparaciones de tablas de la base de datos de distribución o de tablas de metadatos de replicación en una base de datos de distribución, quite la replicación y vuelva a configurarla. Para obtener más información, vea [Deshabilitar la publicación y distribución](../../relational-databases/replication/disable-publishing-and-distribution.md).    
1.  Si el informe de DBCC CHECKDB incluye reparaciones de tablas replicadas, lleve a cabo la validación de datos para determinar dónde se encuentran las diferencias entre los datos de las bases de datos de publicaciones y de suscripciones.    
    
## <a name="result-sets"></a>Conjuntos de resultados    
DBCC CHECKDB devuelve el siguiente conjunto de resultados: Los valores pueden variar, excepto cuando se especifican las opciones ESTIMATEONLY, PHYSICAL_ONLY o NO_INFOMSGS:
    
```
 DBCC results for 'model'.    
    
 Service Broker Msg 9675, Level 10, State 1: Message Types analyzed: 13.    
    
 Service Broker Msg 9676, Level 10, State 1: Service Contracts analyzed: 5.    
    
 Service Broker Msg 9667, Level 10, State 1: Services analyzed: 3.    
    
 Service Broker Msg 9668, Level 10, State 1: Service Queues analyzed: 3.    
    
 Service Broker Msg 9669, Level 10, State 1: Conversation Endpoints analyzed: 0.    
    
 Service Broker Msg 9674, Level 10, State 1: Conversation Groups analyzed: 0.    
    
 Service Broker Msg 9670, Level 10, State 1: Remote Service Bindings analyzed: 0.    
    
 DBCC results for 'sys.sysrowsetcolumns'.    
    
 There are 630 rows in 7 pages for object 'sys.sysrowsetcolumns'.    
    
 DBCC results for 'sys.sysrowsets'.    
    
 There are 97 rows in 1 pages for object 'sys.sysrowsets'.    
    
 DBCC results for 'sysallocunits'.    
    
 There are 195 rows in 3 pages for object 'sysallocunits'.    
    
 There are 0 rows in 0 pages for object "sys.sysasymkeys".    
    
 DBCC results for 'sys.syssqlguides'.    
    
 There are 0 rows in 0 pages for object "sys.syssqlguides".    
    
 DBCC results for 'sys.queue_messages_1977058079'.    
    
 There are 0 rows in 0 pages for object "sys.queue_messages_1977058079".    
    
 DBCC results for 'sys.queue_messages_2009058193'.    
    
 There are 0 rows in 0 pages for object "sys.queue_messages_2009058193".    
    
 DBCC results for 'sys.queue_messages_2041058307'.    
    
 There are 0 rows in 0 pages for object "sys.queue_messages_2041058307".    
    
 CHECKDB found 0 allocation errors and 0 consistency errors in database 'model'.    
    
 DBCC execution completed. If DBCC printed error messages, contact your system administrator.    
```

Si se especifica NO_INFOMSGS, DBCC CHECKDB devuelve el siguiente conjunto de resultados (mensaje):
    
```
 The command(s) completed successfully.
 ```
 
Si se especifica PHYSICAL_ONLY, DBCC CHECKDB devuelve el siguiente conjunto de resultados:
    
```
 DBCC results for 'model'.    
    
 CHECKDB found 0 allocation errors and 0 consistency errors in database 'master'.  
    
 DBCC execution completed. If DBCC printed error messages, contact your system administrator.
 ```
 
Si se especifica ESTIMATEONLY, DBCC CHECKDB devuelve el siguiente conjunto de resultados:
    
```
 Estimated TEMPDB space needed for CHECKALLOC (KB)    
    
 -------------------------------------------------  
    
 13   
    
 (1 row(s) affected)   
    
 Estimated TEMPDB space needed for CHECKTABLES (KB)    
    
 --------------------------------------------------    
    
 57 
    
 (1 row(s) affected)  
    
 DBCC execution completed. If DBCC printed error messages, contact your system administrator.
```
    
## <a name="permissions"></a>Permissions    
Requiere la pertenencia al rol fijo de servidor sysadmin o la función fija de base de datos db_owner.
    
## <a name="examples"></a>Ejemplos    
    
### <a name="a-checking-both-the-current-and-another-database"></a>A. Comprobar la base de datos actual y otra base de datos    
En el ejemplo siguiente se ejecuta `DBCC CHECKDB` para la base de datos actual y para la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].
    
```sql    
-- Check the current database.    
DBCC CHECKDB;    
GO    
-- Check the AdventureWorks2012 database without nonclustered indexes.    
DBCC CHECKDB (AdventureWorks2012, NOINDEX);    
GO    
```    
    
### <a name="b-checking-the-current-database-suppressing-informational-messages"></a>B. Comprobar la base de datos actual, suprimiendo los mensajes informativos    
En el ejemplo siguiente se comprueba la base de datos actual y se suprimen todos los mensajes informativos.
    
```sql    
DBCC CHECKDB WITH NO_INFOMSGS;    
GO    
```    
    
## <a name="see-also"></a>Vea también    
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[Ver el tamaño del archivo disperso de una instantánea de base de datos &#40;Transact-SQL&#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md)  
[sp_helpdb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)  
[Tablas del sistema &#40; Transact-SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  

