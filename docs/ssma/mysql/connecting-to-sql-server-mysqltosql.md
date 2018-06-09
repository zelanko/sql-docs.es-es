---
title: Conectarse a SQL Server (MySQLToSQL) | Documentos de Microsoft
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- connecting to SQL Server 2008, SQL Server permission
- connecting to SQL Server 2008, synchronization
ms.assetid: 08233267-693e-46e6-9ca3-3a3dfd3d2be7
caps.latest.revision: 18
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 20c11888d58557fc340ad39dbeec293e15c555e0
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2018
ms.locfileid: "34775911"
---
# <a name="connecting-to-sql-server-mysqltosql"></a>Conectarse a SQL Server (MySQLToSQL)
Para migrar las bases de datos de MySQL a SQL Server, debe conectarse a la instancia de destino de SQL Server. Cuando se conecta, SSMA obtiene metadatos acerca de todas las bases de datos en la instancia de SQL Server y muestra los metadatos de la base de datos en el Explorador de metadatos de SQL Server. SSMA almacena la información de la instancia de SQL Server están conectados a, pero no almacena las contraseñas.  
  
La conexión a SQL Server sigue activa hasta que se cierra el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse a SQL Server si desea que una conexión activa con el servidor. Puede trabajar sin conexión hasta que se cargará los objetos de base de datos en SQL Server y migrar los datos.  
  
Metadatos acerca de la instancia de SQL Server no se sincronizarán automáticamente. En su lugar, para actualizar los metadatos en el Explorador de metadatos de SQL Server, debe actualizar manualmente los metadatos de SQL Server. Para obtener más información, vea la sección "Sincronizar los metadatos de SQL Server" más adelante en este tema.  
  
## <a name="required-sql-server-permissions"></a>Permisos necesarios de SQL Server  
La cuenta que se usa para conectarse a SQL Server requiere permisos diferentes dependiendo de las acciones que realiza la cuenta:  
  
-   Para convertir objetos de MySQL a [!INCLUDE[tsql](../../includes/tsql_md.md)] secuencias de comandos de sintaxis, para actualizar los metadatos de SQL Server o guardar sintaxis convertida a, la cuenta debe tener permiso para iniciar sesión en la instancia de SQL Server.  
  
-   Para cargar objetos de base de datos en SQL Server, el requisito de permiso mínimo es la pertenencia a la **db_owner** rol de base de datos en la base de datos de destino.  
  
## <a name="establishing-a-sql-server-connection"></a>Establecer una conexión con SQL Server  
Para convertir objetos de base de datos de MySQL a sintaxis de SQL Server, debe establecer una conexión a la instancia de SQL Server donde van a migrar la base de datos de MySQL o bases de datos.  
  
Al definir las propiedades de conexión, también se especifique la base de datos que se migrarán los objetos y datos. Puede personalizar esta asignación en el nivel de esquema de MySQL después de conectarse a SQL Server. Para obtener más información, consulte [asignación de bases de datos de MySQL a SQL Server esquemas &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
> [!IMPORTANT]  
> Antes de intentar conectarse a SQL Server, asegúrese de la instancia de SQL Server se está ejecutando y puede aceptar conexiones.  
  
**Para conectarse a SQL Server**  
  
1.  En el **archivo** menú, seleccione **conectar con SQL Server** (esta opción se habilita después de la creación de un proyecto).  
  
    Si se ha conectado anteriormente a SQL Server, el nombre de comando será **volver a conectar a SQL Server**.  
  
2.  En el cuadro de diálogo de conexión, escriba o seleccione el nombre de la instancia de SQL Server.  
  
    -   Si se conecta a la instancia predeterminada en el equipo local, puede escribir **localhost** o un punto (**.**).  
  
    -   Si se conecta a la instancia predeterminada en otro equipo, escriba el nombre del equipo.  
  
    -   Si se conecta a una instancia con nombre en otro equipo, escriba el nombre del equipo seguido por una barra diagonal inversa y, a continuación, el nombre de instancia, como MyServer\MyInstance.  
  
3.  Si la instancia de SQL Server está configurada para aceptar conexiones en un puerto no predeterminado, escriba el número de puerto que se utiliza para las conexiones de SQL Server en el **puerto del servidor** cuadro. Para la instancia predeterminada de SQL Server, el número de puerto predeterminado es 1433. Para las instancias con nombre, SSMA intentará obtener el número de puerto desde el servicio SQL Server Browser.  
  
4.  En el **autenticación** , seleccione el tipo de autenticación que se usará para la conexión. Para usar la cuenta de Windows actual, seleccione **autenticación de Windows**. Para utilizar un inicio de sesión de SQL Server, seleccione autenticación de SQL Server y, a continuación, proporcione el nombre de inicio de sesión y contraseña.  
  
5.  Para una conexión segura, se agregan dos controles, el **cifrar conexión** y **TrustServerCertificate** casillas de verificación. Solo cuando **cifrar conexión** se activa, el **TrustServerCertificate** casilla de verificación está visible. Cuando **cifrar conexión** está activada (true) y **TrustServerCertificate** está desactivada (false), validará el certificado SSL de SQL Server. Validar el certificado de servidor es una parte del protocolo de enlace de SSL y asegurarse de que el servidor es el apropiado al que hay que conectarse. Para asegurarse de esto, se debe instalar un certificado en el lado del cliente, así como en el servidor.  
  
6.  Haga clic en conectar.  
  
**Mayor compatibilidad de versiones**  
  
Se permite conectar o volver a conectarse a versiones posteriores de SQL Server.  
  
1.  Podrá conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 una vez creado el proyecto [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005.  
  
2.  Podrá conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 una vez creado el proyecto [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 pero no se permite para conectarse a las versiones inferiores, es decir, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005.  
  
3.  Podrá conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 una vez creado el proyecto [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012.  
  
4.  Podrá conectarse a solo [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 una vez creado el proyecto [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014.  
  
5.  Mayor compatibilidad de versión no es válida para "SQL Azure".  
  
||||||||  
|-|-|-|-|-|-|-|  
|**VERSIÓN de servidor de destino de Vs de tipo de proyecto**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005<br /> (Versión: 9.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008<br /> (Versión: 10.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012<br />(Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014<br />(Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016<br />(Version:13.x)|SQL Azure|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005|Sí|Sí|Sí|Sí|Sí||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008||Sí|Sí|Sí|Sí||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012|||Sí|Sí|Sí||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2014||||Sí|Sí||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2016|||||Sí||  
|SQL Azure||||||Sí|  
  
> [!IMPORTANT]  
> Conversión de los objetos de base de datos se lleva a cabo según el tipo de proyecto, pero no según la versión de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] conectado a. En caso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] proyecto 2005, conversión se lleva a cabo según [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005 incluso si está conectado a una versión más reciente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] (SQL Server 2008 y SQL Server 2012 y SQL Server 2014/SQL Server 2016).  
  
## <a name="synchronizing-sql-server-metadata"></a>Sincronizar los metadatos de SQL Server  
Metadatos acerca de las bases de datos de SQL Server no se actualizan automáticamente. Los metadatos en el Explorador de metadatos de SQL Server están una instantánea de los metadatos cuando conectó por primera vez en SQL Server o la última vez que usted manualmente han actualizado los metadatos. Puede actualizar manualmente los metadatos para todas las bases de datos, o para cualquier base de datos u objeto de base de datos.  
  
**Para sincronizar los metadatos**  
  
1.  Asegúrese de que está conectado a SQL Server.  
  
2.  En el Explorador de metadatos de SQL Server, active la casilla de verificación junto a la base de datos o el esquema de base de datos que desea actualizar.  
  
    Por ejemplo, para actualizar los metadatos de todas las bases de datos, active la casilla situada junto a las bases de datos.  
  
3.  Haga clic en bases de datos, o la base de datos individual o el esquema de base de datos y, a continuación, seleccione **sincronizar con la base de datos**.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso de la migración depende de las necesidades del proyecto:  
  
-   Para personalizar la asignación entre los esquemas y las bases de datos de SQL Server y MySQL esquemas, vea [bases de datos de asignación de MySQL a SQL Server esquemas &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
-   Para personalizar las opciones de configuración para los proyectos, vea [establecer las opciones del proyecto &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)  
  
-   Para personalizar la asignación de tipos de datos de origen y de destino, vea [MySQL de asignación y tipos de datos de SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   Si no tiene que realizar cualquiera de estas tareas, puede convertir las definiciones de objeto de base de datos MySQL en definiciones de objetos de SQL Server. Para obtener más información, consulte [convertir bases de datos de MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>Vea también  
[Bases de datos de migración desde MySQL a SQL Server: base de datos de SQL Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
