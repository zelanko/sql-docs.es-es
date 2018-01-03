---
title: Conectarse a SQL Server (SybaseToSQL) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-sybase
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords: Connecting to SQL Server
ms.assetid: dd368a1a-45b0-40e9-b4d3-5cdb48c26606
caps.latest.revision: "15"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 222e32803e197a18d47c7bf65b76de3f8d24fa15
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="connecting-to-sql-server-sybasetosql"></a>Conectarse a SQL Server (SybaseToSQL)
Migrar bases de datos de Sybase Adaptive Server Enterprise (ASE) a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], debe conectarse a cualquiera de las instancias de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Cuando se conecta, SSMA obtiene metadatos acerca de todas las bases de datos en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y muestra los metadatos de la base de datos en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Explorador de metadatos. SSMA almacena información acerca de qué instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] están conectados a, pero no almacena las contraseñas.  
  
La conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] permanece activo hasta que se cierra el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] si desea que una conexión activa con el servidor. Puede trabajar sin conexión hasta que carga los objetos de base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y migrar los datos.  
  
Metadatos acerca de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] no se sincronizará automáticamente. En su lugar, si desea actualizar los metadatos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] el Explorador de metadatos, debe actualizar manualmente el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] metadatos, como se describe en la "Synchronizing [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] metadatos" más adelante en este tema.  
  
## <a name="required-sql-server-permissions"></a>Permisos necesarios de SQL Server  
La cuenta que se usa para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] requiere permisos diferentes dependiendo de las acciones realizadas por esa cuenta.  
  
-   Para convertir objetos de ASE a [!INCLUDE[tsql](../../includes/tsql_md.md)] sintaxis, para actualizar los metadatos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], o para guardar sintaxis convertidos en scripts, la cuenta debe tener permiso para iniciar sesión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   Para cargar los objetos de base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], el requisito de permiso mínimo es la pertenencia a la **db_owner** rol de base de datos en la base de datos de destino.  
  
-   Para migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], la cuenta debe ser miembro de la **sysadmin** rol de servidor. Esto es necesario para ejecutar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] paquetes de agente de migración de datos.  
  
-   Para ejecutar el código generado por SSMA, la cuenta debe tener **Execute** permisos para todas las funciones definidas por el usuario en el **ssma_syb** esquema de la **sysdb** base de datos. Estas funciones proporcionan una funcionalidad equivalente ASE de funciones del sistema y se utilizan por objetos convertidos.  
  
Si la cuenta que se usa para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] es realizar la migración de todas las tareas, la cuenta debe ser un miembro de la **sysadmin** rol de servidor.  
  
## <a name="establishing-a-sql-server-connection"></a>Establecer una conexión con SQL Server  
Antes de convertir objetos de base de datos de ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sintaxis, debe establecer una conexión a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] donde van a migrar la base de datos de ASE o bases de datos.  
  
Al definir las propiedades de conexión, también se especifique la base de datos que se migrarán los objetos y datos. Puede personalizar esta asignación en el nivel de esquema ASE después de conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para obtener más información, vea [asignación Sybase ASE esquemas para esquemas de SQL Server &#40; SybaseToSQL &#41; ](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md).  
  
> [!IMPORTANT]  
> Antes de intentar conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], asegúrese de que la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se está ejecutando y puede aceptar conexiones.  
  
**Para conectarse a SQL Server**  
  
1.  En el **archivo** menú, seleccione **conectar con SQL Server**.  
  
    Si se ha conectado anteriormente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], será el nombre del comando **volver a conectar a SQL Server**.  
  
2.  En el cuadro de diálogo de conexión, escriba o seleccione el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
    -   Si se conecta a la instancia predeterminada en el equipo local, puede escribir **localhost** o un punto (**.**).  
  
    -   Si se conecta a la instancia predeterminada en otro equipo, escriba el nombre del equipo.  
  
    -   Si se conecta a una instancia con nombre en otro equipo, escriba el nombre del equipo seguido por una barra diagonal inversa y, a continuación, el nombre de instancia, como MyServer\MyInstance.  
  
3.  Si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] está configurado para aceptar conexiones en un puerto no predeterminado, escriba el número de puerto que se utiliza para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] conexiones en el **puerto del servidor** cuadro. Para la instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], el número de puerto predeterminado es 1433. Para las instancias con nombre, SSMA intentará obtener el número de puerto desde el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] servicio Browser.  
  
4.  En el **base de datos** cuadro, escriba el nombre de la base de datos de destino.  
  
    Esta opción no está disponible cuando vuelve a conectar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
5.  En el **autenticación** , seleccione el tipo de autenticación que se usará para la conexión. Para usar la cuenta de Windows actual, seleccione **autenticación de Windows**. Para usar un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] inicio de sesión, seleccione **autenticación de SQL Server** y, a continuación, proporcione el nombre de inicio de sesión y una contraseña.  
  
6.  Para una conexión segura, se agregan dos controles, el **cifrar conexión** y **TrustServerCertificate** casillas de verificación. Solo cuando **cifrar conexión** se activa, el **TrustServerCertificate** casilla de verificación está visible. Cuando **cifrar conexión** está activada (true) y **TrustServerCertificate** está desactivada (false), validará el certificado SSL de SQL Server. Validar el certificado de servidor es una parte del protocolo de enlace de SSL y asegurarse de que el servidor es el apropiado al que hay que conectarse. Para asegurarse de esto, se debe instalar un certificado en el lado del cliente, así como en el servidor.  
  
7.  Haga clic en **Conectar**.  
  
**Mayor compatibilidad de versión**  
  
-   Podrá conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 una vez creado el proyecto de migración [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005.  
  
-   Podrá conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 una vez creado el proyecto de migración [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 pero no podrán conectarse a las versiones inferiores, es decir, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005.  
  
-   Podrá conectarse a solo [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 cuando el proyecto creado es SQL Server 2012.  
  
-   Mayor compatibilidad de versión no es válida para SQL Azure.  
  
||||||||
|-|-|-|-|-|-|-|
|**VERSIÓN de servidor de destino de Vs de tipo de proyecto**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005<br /> (Versión: 9.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008<br /> (Versión: 10.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 <br />(Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 <br />(Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 <br />(Version:13.x)|SQL Azure|
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005|Sí|Sí|Sí|Sí|Sí||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008||Sí|Sí|Sí|Sí||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012|||Sí|Sí|Sí||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014||||Sí|Sí|| 
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016|||||Sí||  
|SQL Azure||||||Sí|  
  
> [!IMPORTANT]  
> Conversión de los objetos de base de datos se lleva a cabo según el tipo de proyecto, pero no según la versión de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] que está conectado. En caso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] proyecto 2005, conversión se lleva a cabo según [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005 incluso si está conectado a una versión más reciente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ([!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016)  
  
## <a name="reconnecting-to-sql-server"></a>Volver a conectarse a SQL Server  
La conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] permanece activo hasta que se cierra el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] si desea que una conexión activa con el servidor. Puede trabajar sin conexión hasta que actualice los metadatos, objetos de base de datos de carga en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], y migrar los datos.  
  
El procedimiento para volver a conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] es el mismo que el procedimiento para establecer una conexión.  
  
## <a name="synchronizing-sql-server-metadata"></a>Sincronizar los metadatos de SQL Server  
Metadatos sobre el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bases de datos no se actualiza automáticamente. Los metadatos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Explorador de metadatos es una instantánea de los metadatos cuando conectó por primera vez a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], o la última vez que se han actualizado manualmente los metadatos. Puede actualizar manualmente los metadatos para todas las bases de datos, o para cualquier base de datos u objeto de base de datos.  
  
**Para sincronizar los metadatos**  
  
1.  Asegúrese de que están conectados a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
2.  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] el Explorador de metadatos, active la casilla situada junto a la base de datos o esquema que desea actualizar la base de datos.  
  
    Por ejemplo, para actualizar los metadatos de todas las bases de datos, seleccione junto a la casilla de **bases de datos**.  
  
3.  Haga clic en las bases de datos o la base de datos individual o el esquema de base de datos y, a continuación, seleccione **sincronizar con la base de datos**.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso de la migración depende de las necesidades del proyecto:  
  
-   Si desea personalizar la asignación entre los esquemas y las bases de datos de ASE y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bases de datos y esquemas, vea [esquemas de asignación Sybase ASE para esquemas de SQL Server &#40; SybaseToSQL &#41; ](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md).  
  
-   Si desea personalizar las opciones de configuración para los proyectos, vea [establecer las opciones del proyecto &#40; SybaseToSQL &#41; ](../../ssma/sybase/setting-project-options-sybasetosql.md).  
  
-   Si quiere personalizado a la asignación de tipos de datos de origen y de destino, vea [asignación Sybase ASE y tipos de datos de SQL Server &#40; SybaseToSQL &#41; ](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
-   Si no es necesario realizar alguna de estas, se pueden convertir las definiciones de objeto de base de datos de Sybase ASE en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] definiciones de objetos. Para obtener más información, vea [convertir objetos de base de datos de Sybase ASE &#40; SybaseToSQL &#41; ](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md).  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de ASE de Sybase a SQL Server: base de datos de SQL Azure &#40; SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
