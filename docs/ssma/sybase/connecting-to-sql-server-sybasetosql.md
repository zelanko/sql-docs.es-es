---
title: Conexión a SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to SQL Server
ms.assetid: dd368a1a-45b0-40e9-b4d3-5cdb48c26606
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 318de1e7a463892dbb40639bccacb89f6907b8bf
ms.sourcegitcommit: 21bedbae28840e2f96f5e8b08bcfc794f305c8bc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2020
ms.locfileid: "87864772"
---
# <a name="connecting-to-sql-server-sybasetosql"></a>Conexión a SQL Server (SybaseToSQL)
Para migrar las bases de datos de Sybase Adaptive Server Enterprise (ASE) a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe conectarse a cualquiera de las instancias de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Cuando se conecta, SSMA obtiene los metadatos de todas las bases de datos de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y muestra los metadatos de la base de datos en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Explorador de metadatos. SSMA almacena información acerca de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la que está conectado, pero no almacena contraseñas.  
  
La conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permanece activa hasta que se cierra el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si desea una conexión activa con el servidor. Puede trabajar sin conexión hasta que cargue los objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de base de datos en y migre los datos.  
  
Los metadatos de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se sincronizan automáticamente. En su lugar, si desea actualizar los metadatos en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Explorador de metadatos, debe actualizar manualmente los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadatos, como se describe en la sección "sincronizar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadatos" más adelante en este tema.  
  
## <a name="required-sql-server-permissions"></a>Permisos SQL Server necesarios  
La cuenta que se usa para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requiere permisos diferentes en función de las acciones realizadas por esa cuenta.  
  
-   Para convertir objetos ASE en [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxis, actualizar metadatos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o guardar la sintaxis convertida en scripts, la cuenta debe tener permiso para iniciar sesión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Para cargar los objetos de base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el requisito de permiso mínimo es la pertenencia al rol de base de datos **db_owner** en la base de datos de destino.  
  
-   Para migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , la cuenta debe ser miembro del rol de servidor **sysadmin** . Esto es necesario para ejecutar los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] paquetes de migración de datos del agente.  
  
-   Para ejecutar el código generado por SSMA, la cuenta debe tener permisos de **ejecución** para todas las funciones definidas por el usuario en el esquema de **ssma_syb** de la base de datos **sysdb** . Estas funciones proporcionan una funcionalidad equivalente de las funciones del sistema ASE y las usan los objetos convertidos.  
  
Si la cuenta que se usa para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es realizar todas las tareas de migración, la cuenta debe ser miembro del rol de servidor **sysadmin** .  
  
## <a name="establishing-a-sql-server-connection"></a>Establecer una conexión SQL Server  
Antes de convertir los objetos de base [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de datos de ase a sintaxis, debe establecer una conexión con la instancia de en la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que desea migrar la base de datos o las bases de datos de ase.  
  
Al definir las propiedades de conexión, también se especifica la base de datos en la que se migrarán los objetos y los datos. Puede personalizar esta asignación en el nivel de esquema de ASE después de conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, consulte [asignación de esquemas de Sybase ase a esquemas de SQL Server &#40;&#41;SybaseToSQL ](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md).  
  
> [!IMPORTANT]  
> Antes de intentar conectarse a, asegúrese de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se está ejecutando y puede aceptar conexiones.  
  
**Para conectarse a SQL Server**  
  
1.  En el menú **archivo** , seleccione **conectarse a SQL Server**.  
  
    Si anteriormente se conectó a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el nombre del comando se volverá **a conectar a SQL Server**.  
  
2.  En el cuadro de diálogo conexión, escriba o seleccione el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    -   Si se está conectando a la instancia predeterminada en el equipo local, puede especificar **localhost** o un punto (**.**).  
  
    -   Si se va a conectar a la instancia predeterminada en otro equipo, escriba el nombre del equipo.  
  
    -   Si se va a conectar a una instancia con nombre en otro equipo, escriba el nombre del equipo seguido de una barra diagonal inversa y, a continuación, el nombre de la instancia, como MyServer\MyInstance.  
  
3.  Si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está configurada para aceptar conexiones en un puerto no predeterminado, escriba el número de puerto que se utiliza para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] las conexiones en el cuadro **Puerto del servidor** . Para la instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el número de puerto predeterminado es 1433. En el caso de las instancias con nombre, SSMA intentará obtener el número de puerto del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio explorador.  
  
4.  En el cuadro **base de datos** , escriba el nombre de la base de datos de destino.  
  
    Esta opción no está disponible cuando se vuelve a conectar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
5.  En el cuadro **autenticación** , seleccione el tipo de autenticación que se utilizará para la conexión. Para usar la cuenta de Windows actual, seleccione **autenticación de Windows**. Para usar un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Inicio de sesión de, seleccione **autenticación de SQL Server** y, a continuación, proporcione el nombre y la contraseña de inicio de sesión.  
  
6.  Para una conexión segura, se agregan dos controles, las casillas de verificación **cifrar conexión** y **TrustServerCertificate** . Solo cuando se activa **cifrar conexión** , la casilla **TrustServerCertificate** está visible. Cuando se activa la opción **cifrar conexión** (true) y **TrustServerCertificate** está desactivado (false), se validará el certificado SSL SQL Server. Validar el certificado de servidor es una parte del protocolo de enlace de SSL y asegurarse de que el servidor es el apropiado al que hay que conectarse. Para garantizar esto, se debe instalar un certificado en el lado cliente y en el lado servidor.  
  
7.  Haga clic en **Conectar**.  
  
**Mayor compatibilidad de versiones**  
  
-   Podrá conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 cuando el proyecto de migración creado sea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
-   Podrá conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 cuando el proyecto de migración creado sea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, pero no podrá conectarse a las versiones anteriores, es decir, a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
-   Solo podrá conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 cuando el proyecto creado sea SQL Server 2012.  
  
-   La compatibilidad con versiones posteriores no es válida para SQL Azure.  
  
|TIPO de proyecto frente a versión del servidor de destino|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005<br /> (Versión: 9. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008<br /> (Versión: 10. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 <br />(Versión: 11. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 <br />(Versión: 12. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 <br />(Versión: 13. x)|SQL Azure|
|-|-|-|-|-|-|-|
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|Sí|Sí|Sí|Sí|Sí||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||Sí|Sí|Sí|Sí||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||Sí|Sí|Sí||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014||||Sí|Sí|| 
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|||||Sí||  
|SQL Azure||||||Sí|  
  
> [!IMPORTANT]
> La conversión de los objetos de base de datos se realiza según el tipo de proyecto, pero no según la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la que esté conectado. En el caso del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proyecto 2005, la conversión se realiza según [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005, aunque esté conectado a una versión posterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016)  
  
## <a name="reconnecting-to-sql-server"></a>Volver a conectar a SQL Server  
La conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permanece activa hasta que se cierra el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si desea una conexión activa con el servidor. Puede trabajar sin conexión hasta que actualice los metadatos, cargue los objetos de base de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos en y migre los datos.  
  
El procedimiento para volver a conectar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es el mismo que el procedimiento para establecer una conexión.  
  
## <a name="synchronizing-sql-server-metadata"></a>Sincronizar metadatos de SQL Server  
Los metadatos de las bases de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se actualizan automáticamente. Los metadatos del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Explorador de metadatos son una instantánea de los metadatos al conectarse por primera vez a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o la última vez que se actualizaron los metadatos manualmente. Puede actualizar manualmente los metadatos de todas las bases de datos o de cualquier base de datos o objeto de base de datos.  
  
**Para sincronizar los metadatos**  
  
1.  Asegúrese de que está conectado a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  En el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Explorador de metadatos, active la casilla situada junto a la base de datos o el esquema de la base de datos que desea actualizar.  
  
    Por ejemplo, para actualizar los metadatos de todas las bases de datos, active la casilla situada junto a **bases**de datos.  
  
3.  Haga clic con el botón derecho en bases de datos o en el esquema de base de datos o de base de datos individual y seleccione **sincronizar con base de datos**.  
  
## <a name="next-step"></a>siguiente paso  
El siguiente paso de la migración depende de las necesidades del proyecto:  
  
-   Si desea personalizar la asignación entre las bases de datos de ASE y los esquemas y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] las bases de datos y los esquemas, consulte [asignación de esquemas de Sybase ase a esquemas de SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md).  
  
-   Si desea personalizar las opciones de configuración de los proyectos, vea [establecer opciones de proyecto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md).  
  
-   Si desea personalizar la asignación de los tipos de datos de origen y de destino, consulte [asignación de tipos de datos de Sybase ase y SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
-   Si no tiene que realizar ninguna de estas tareas, puede convertir las definiciones de objetos de base de datos de Sybase ASE en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definiciones de objeto. Para obtener más información, consulte [conversión de objetos de base de datos de Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md).  
  
## <a name="see-also"></a>Consulte también  
[Migración de bases de datos de Sybase ASE a SQL Server Azure SQL Database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
