---
title: Suscriptores de IBM DB2 | Microsoft Docs
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- non-SQL Server Subscribers, IBM DB2
- data types [SQL Server replication], non-SQL Server Subscribers
- IBM DB2 Subscribers
- mapping data types [SQL Server replication]
- heterogeneous Subscribers, IBM DB2
ms.assetid: a1a27b1e-45dd-4d7d-b6c0-2b608ed175f6
caps.latest.revision: "74"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 402675d8725ca5e571261e700b9eb8ec2a035a90
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="ibm-db2-subscribers"></a>IBM DB2 Subscribers
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admite suscripciones de inserción a IBM DB2/AS 400, DB2/MVS y DB2/Universal Database a través de los proveedores de OLE DB incluidos con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Host Integration Server.  
  
## <a name="configuring-an-ibm-db2-subscriber"></a>Configuración de un suscriptor de IBM DB2  
 Para configurar un suscriptor de IBM DB2, siga estos pasos:  
  
1.  Instale la versión más reciente del proveedor OLE DB de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] para DB2 en el distribuidor:  
  
    -   Si usa [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] Enterprise Edition, en la página web [Descargas de SQL Server](http://go.microsoft.com/fwlink/?LinkId=149256), en la sección de **descargas relacionadas**, haga clic en el vínculo a la versión más reciente de Microsoft SQL Server Feature Pack. En la página web **Microsoft SQL Server Feature Pack**, busque **Proveedor OLE DB de Microsoft para DB2**.  
  
    -   Si usa [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] Standard Edition, instale la versión más reciente del servidor [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Host [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] (HIS), que contiene el proveedor.  
  
     Además de instalar el proveedor, se recomienda instalar la Herramienta de acceso a datos, que se utiliza en el paso siguiente (se instala de manera predeterminada con la descarga de [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] Enterprise Edition). Para obtener más información sobre la instalación y uso de la Herramienta de acceso a datos, vea la documentación del proveedor o de HIS.  
  
2.  Cree una cadena de conexión para el suscriptor. La cadena de conexión se puede crear en cualquier editor de texto, pero se recomienda utilizar la Herramienta de acceso a datos. Para crear la cadena en la Herramienta de acceso a datos:  
  
    1.  Haga clic en **Inicio**, **Programas**, **Proveedor Microsoft OLE DB para DB2**y, a continuación, en **Herramienta de acceso a datos**.  
  
    2.  Siga los pasos que se indican en la **Herramienta de acceso a datos**para obtener información acerca del servidor DB2. Al completar la herramienta, se crea un vínculo de datos universal (UDL) con una cadena de conexión asociada (el UDL no se usa realmente en la replicación, pero la cadena de conexión sí).  
  
    3.  Obtenga acceso a la cadena de conexión: haga clic con el botón secundario en el UDL en la Herramienta de acceso a datos y seleccione **Display Connection String**(Mostrar cadena de conexión).  
  
     La cadena de conexión será similar a la siguiente (los saltos de línea son para facilitar la lectura):  
  
    ```  
    Provider=DB2OLEDB;Initial Catalog=MY_SUBSCRIBER_DB;Network Transport Library=TCP;Host CCSID=1252;  
    PC Code Page=1252;Network Address=MY_SUBSCRIBER;Network Port=50000;Package Collection=MY_PKGCOL;  
    Default Schema=MY_SCHEMA;Process Binary as Character=False;Derive Parameters=False;Units of Work=RUW;DBMS Platform=DB2/NT;  
    Persist Security Info=False;Connection Pooling=True;  
    ```  
  
     La mayoría de las opciones de la cadena son específicas para el servidor DB2 que está configurando, pero las opciones `Process Binary as Character` y `Derive Parameters` siempre deben establecerse en `False`. Se requiere un valor para que la opción `Initial Catalog` identifique la base de datos de suscripciones. La cadena de conexión se insertará en el Asistente para nueva suscripción cuando se cree la suscripción.  
  
3.  Cree una instantánea o una publicación transaccional, habilítela para suscriptores que no sean[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y, después, cree una suscripción de inserción para el suscriptor. Para más información, consulte [Crear una suscripción para un suscriptor que no sea de SQL Server](../../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md).  
  
4.  O bien, especifique un script de creación personalizado para uno o más artículos. Cuando se publica la tabla, se crea un script `CREATE TABLE` para ella. Para los suscriptores que no son de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , el script se crea en dialecto de [!INCLUDE[tsql](../../../includes/tsql-md.md)] y, posteriormente, el Agente de distribución lo convierte a un dialecto SQL más general antes de aplicarlo en el suscriptor. Para especificar un script de creación personalizado, modifique el script [!INCLUDE[tsql](../../../includes/tsql-md.md)] existente o cree un script completo que utilice el dialecto DB2 SQL; si crea un script DB2, use la directiva **bypass_translation** para que el Agente de distribución aplique el script sin convertir en el suscriptor.  
  
     Los scripts se pueden modificar por distintas razones, aunque la más común es para modificar las asignaciones de tipos de datos. Para obtener más información, vea la sección "Consideraciones acerca de la asignación de tipos de datos", en este tema. Si modifica el script [!INCLUDE[tsql](../../../includes/tsql-md.md)] , los cambios deben limitarse a cambios en la asignación de tipos de datos y el script no debe contener ningún comentario. Si se necesitan cambios más importantes, cree un script DB2.  
  
     **Para modificar el script de un artículo y suministrarlo como un script de creación personalizado**  
  
    1.  Una vez generada la instantánea para la publicación, navegue a la carpeta de instantáneas de la publicación.  
  
    2.  Busque el archivo `.sch` que tiene el mismo nombre que el artículo; por ejemplo, `MyArticle.sch`.  
  
    3.  Abra este archivo en el Bloc de notas o en otro editor de texto.  
  
    4.  Modifique el archivo y guárdelo en un directorio distinto.  
  
    5.  Ejecute `sp_changearticle`, especificando la ruta de acceso del archivo y el nombre de la propiedad *creation_script* . Para más información, vea [sp_changearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md).  
  
     **Para crear un script de un artículo y suministrarlo como un script de creación personalizado**  
  
    1.  Cree un script de artículo con el dialecto DB2 SQL. Asegúrese de que la primera línea del archivo sea **bypass_translation**y de que no haya nada más en la línea.  
  
    2.  Ejecute sp_changearticle, especificando la ruta de acceso del archivo y el nombre de la propiedad *creation_script*.  
  
## <a name="considerations-for-ibm-db2-subscribers"></a>Consideraciones para los suscriptores de IBM DB2  
 Además de las consideraciones planteadas en el tema [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md), tenga en cuenta los siguientes problemas al replicar en suscriptores de DB2:  
  
-   Los datos y los índices para cada tabla replicada se asignan a un espacio de tablas de DB2. El tamaño de la página de un espacio de tablas de DB2 controla el número máximo de columnas y el tamaño máximo de las filas de las tablas que pertenecen al espacio de tablas. Asegúrese de que el espacio de tablas asociado con las tablas replicadas es apropiado para el número de columnas replicadas y el tamaño máximo de las filas de las tablas.  
  
-   No publique tablas en suscriptores de DB2 con la replicación transaccional si una o más columnas de clave principal en la tabla tienen un tipo de datos DECIMAL(32-38, 0-38) o NUMERIC(32-38, 0-38). La replicación transaccional identifica las filas con la clave principal y esto puede producir errores, ya que estos tipos de datos se asignan a VARCHAR(41) en el suscriptor. Las tablas con claves principales que utilicen estos tipos de datos se pueden publicar con la replicación de instantáneas.  
  
-   Si desea crear previamente las tablas en el suscriptor en lugar de crearlas por medio de la replicación, use la opción Solo compatibilidad con replicación. Para obtener más información, consulte [Initialize a Transactional Subscription Without a Snapshot](../../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permite utilizar nombres de tabla y de columna más largos que DB2:  
  
    -   Si la base de datos de publicación incluye tablas con nombres más largos que los admitidos por la versión de DB2 en el suscriptor, especifique otro nombre para la propiedad destination_table del artículo. Para más información sobre cómo configurar propiedades al crear una publicación, vea [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md) (Crear una publicación) y [Define an Article](../../../relational-databases/replication/publish/define-an-article.md) (Definir un artículo).  
  
    -   No es posible especificar otros nombres de columnas. Debe asegurarse de que las tablas publicadas no incluyan nombres de columna más largos que lo permitido por la versión de DB2 en el suscriptor.  
  
## <a name="mapping-data-types-from-sql-server-to-ibm-db2"></a>Asignar tipos de datos de SQL Server a IBM DB2  
 En la tabla siguiente se muestran las asignaciones de tipos de datos que se utilizan cuando se replican datos en un suscriptor que ejecuta IBM DB2.  
  
|Tipo de datos de SQL Server|Tipo de datos de IBM DB2|  
|--------------------------|-----------------------|  
|**bigint**|DECIMAL(19,0)|  
|**binary(1-254)**|CHAR(1-254) FOR BIT DATA|  
|**binary(255-8000)**|VARCHAR(255-8000) FOR BIT DATA|  
|**bit**|SMALLINT|  
|**char(1-254)**|CHAR(1-254)|  
|**char(255-8000)**|VARCHAR(255-8000)|  
|**date**|DATE|  
|**datetime**|timestamp|  
|**datetime2(0-7)**|VARCHAR(27)|  
|**datetimeoffset(0-7)**|VARCHAR(34)|  
|**decimal(1-31, 0-31)**|DECIMAL(1-31, 0-31)|  
|**decimal(32-38, 0-38)**|VARCHAR(41)|  
|**float(53)**|DOUBLE|  
|**float**|FLOAT|  
|**geography**|IMAGE|  
|**geometry**|IMAGE|  
|**hierarchyid**|IMAGE|  
|**image**|VARCHAR(0) FOR BIT DATA*|  
|**into**|INT|  
|**money**|DECIMAL(19,4)|  
|**nchar(1-4000)**|VARCHAR(1-4000)|  
|**nvarchar(max)**|VARCHAR(0)*|  
|**numeric(1-31, 0-31)**|DECIMAL(1-31,0-31)|  
|**numeric(32-38, 0-38)**|VARCHAR(41)|  
|**nvarchar(1-4000)**|VARCHAR(1-4000)|  
|**ssNoVersion**|VARCHAR(0)*|  
|**real**|real|  
|**smalldatetime**|timestamp|  
|**smallint**|SMALLINT|  
|**smallmoney**|DECIMAL(10,4)|  
|**sql_variant**|N/D|  
|**sysname**|VARCHAR(128)|  
|**varchar(max)**|VARCHAR(0)*|  
|**time(0-7)**|VARCHAR(16)|  
|**timestamp**|CHAR(8) FOR BIT DATA|  
|**tinyint**|SMALLINT|  
|**uniqueidentifier**|CHAR(38)|  
|**varbinary(1-8000)**|VARCHAR(1-8000) FOR BIT DATA|  
|**varchar(1-8000)**|VARCHAR(1-8000)|  
|**varbinary(max)**|VARCHAR(0) FOR BIT DATA*|  
|**ntext**|VARCHAR(0)*|  
|**xml**|VARCHAR(0)*|  
  
* Para más información sobre las asignaciones a VARCHAR(0), vea la siguiente sección.  
  
### <a name="data-type-mapping-considerations"></a>Consideraciones acerca de la asignación de tipos de datos  
 Tenga en cuenta los siguientes problemas de asignación de tipos de datos al replicar en suscriptores de DB2:  
  
-   Al asignar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **char**, **varchar**, **binary** y **varbinary** a CHAR, VARCHAR, CHAR FOR BIT DATA y VARCHAR FOR BIT DATA de DB2, respectivamente, la replicación establece la longitud del tipo de datos de DB2 de forma que sea igual a la del tipo de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
     Esto permite crear correctamente la tabla generada en el suscriptor, siempre que la restricción del tamaño de página de DB2 sea suficientemente grande como para admitir el tamaño máximo de la fila. Asegúrese de que el nombre de inicio de sesión que utiliza para obtener acceso a la base de datos de DB2 tiene permisos de acceso a espacios de tabla de tamaño suficiente para las tablas que se van a replicar en DB2.  
  
-   DB2 admite columnas VARCHAR de hasta 32 kilobytes (KB); por lo tanto, es posible que algunas columnas de objetos grandes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se puedan asignar correctamente a columnas VARCHAR de DB2. Sin embargo, el proveedor OLE DB que utiliza la replicación para DB2 no admite la asignación de objetos grandes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a objetos grandes de DB2. Por este motivo, las columnas de tipo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **varchar(max)**, **ntext**, **nvarchar(max)**de **ssNoVersion** se asignan a VARCHAR(0) en los scripts de creación generados. El valor de longitud 0 debe cambiarse a un valor apropiado antes de aplicar el script al suscriptor. Si no se cambia la longitud del tipo de datos, DB2 mostrará el error 604 cuando se intente crear la tabla en el suscriptor de DB2 (el error 604 indica que la precisión o el atributo de longitud de un tipo de datos no son válidos).  
  
     Basándose en sus conocimientos de la tabla de origen que desea replicar, determine si es apropiado asignar un objeto grande de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a un elemento de longitud variable de DB2 y especifique una longitud máxima apropiada en un script de creación personalizado. Para obtener información acerca de cómo especificar un script de creación personalizado, vea el paso 5 de la sección "Configuración de un suscriptor de IBM DB2", en este tema.  
  
    > [!NOTE]  
    >  La longitud especificada para el tipo DB2, al combinarse con otras longitudes de columna, no puede superar el tamaño máximo de fila especificado, basado en el espacio de tabla de DB2 al que están asignados los datos de la tabla.  
  
     Si no hay ninguna asignación apropiada para una columna de objetos grandes, puede utilizar el filtrado de columna en el artículo para que no se replique. Para obtener más información, vea [Filtrar datos publicados](../../../relational-databases/replication/publish/filter-published-data.md).  
  
-   Al replicar los tipos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **nvarchar** y **ssNoVersion** en CHAR y VARCHAR de DB2, la replicación utiliza el mismo especificador de longitud para el tipo de DB2 que para el de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Sin embargo, es posible que la longitud del tipo de datos sea demasiado reducida para la tabla DB2 generada.  
  
     En algunos entornos de DB2, un elemento de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **char** no se limita a caracteres de un solo byte; esto debe tenerse en cuenta para la longitud de un elemento CHAR o VARCHAR. También debe tener en cuenta los caracteres de *desplazamiento hacia dentro* y *desplazamiento hacia fuera* si se necesitan. Si desea replicar tablas con columnas **nchar** y **nvarchar** , es posible que necesite especificar una longitud máxima mayor para el tipo de datos en un script de creación personalizado. Para obtener información acerca de cómo especificar un script de creación personalizado, vea el paso 5 de la sección "Configuración de un suscriptor de IBM DB2", en este tema.  
  
## <a name="see-also"></a>Ver también  
 [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [Suscribirse a publicaciones](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  
