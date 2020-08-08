---
title: Conexión a SQL Server (MySQLToSQL) | Microsoft Docs
description: Obtenga información sobre cómo conectarse a una instancia de destino de SQL Server para migrar bases de datos de MySQL. SSMA obtiene metadatos acerca de las bases de datos en SQL Server.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- connecting to SQL Server 2008, SQL Server permission
- connecting to SQL Server 2008, synchronization
ms.assetid: 08233267-693e-46e6-9ca3-3a3dfd3d2be7
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 548433b02590ccacf164e9479690f1adadbbc3c4
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2020
ms.locfileid: "87936288"
---
# <a name="connecting-to-sql-server-mysqltosql"></a>Conexión a SQL Server (MySQLToSQL)
Para migrar las bases de datos de MySQL a SQL Server, debe conectarse a la instancia de destino de SQL Server. Cuando se conecta, SSMA obtiene los metadatos de todas las bases de datos de la instancia de SQL Server y muestra los metadatos de la base de datos en el explorador de metadatos de SQL Server. SSMA almacena información de la instancia de SQL Server a la que está conectado, pero no almacena contraseñas.  
  
La conexión a SQL Server permanece activa hasta que se cierra el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse a SQL Server si desea una conexión activa con el servidor. Puede trabajar sin conexión hasta que cargue los objetos de base de datos en SQL Server y migre los datos.  
  
Los metadatos sobre la instancia de SQL Server no se sincronizan automáticamente. En su lugar, para actualizar los metadatos en SQL Server explorador de metadatos, debe actualizar manualmente los metadatos de SQL Server. Para obtener más información, vea la sección "sincronizar metadatos de SQL Server" más adelante en este tema.  
  
## <a name="required-sql-server-permissions"></a>Permisos SQL Server necesarios  
La cuenta que se usa para conectarse a SQL Server requiere permisos diferentes en función de las acciones que realiza la cuenta:  
  
-   Para convertir objetos MySQL en [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxis, actualizar metadatos de SQL Server o guardar la sintaxis convertida en scripts, la cuenta debe tener permiso para iniciar sesión en la instancia de SQL Server.  
  
-   Para cargar los objetos de base de datos en SQL Server, el requisito de permiso mínimo es la pertenencia al rol de base de datos **db_owner** en la base de datos de destino.  
  
## <a name="establishing-a-sql-server-connection"></a>Establecer una conexión SQL Server  
Antes de convertir los objetos de base de datos de MySQL en SQL Server sintaxis, debe establecer una conexión con la instancia de SQL Server en la que desea migrar la base de datos o las bases de datos de MySQL.  
  
Al definir las propiedades de conexión, también se especifica la base de datos en la que se migrarán los objetos y los datos. Puede personalizar esta asignación en el nivel de esquema de MySQL después de conectarse a SQL Server. Para obtener más información, consulte [asignación de bases de datos de MySQL a esquemas de SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
> [!IMPORTANT]  
> Antes de intentar conectarse a SQL Server, asegúrese de que la instancia de SQL Server se está ejecutando y puede aceptar conexiones.  
  
**Para conectarse a SQL Server**  
  
1.  En el menú **archivo** , seleccione **conectarse a SQL Server** (esta opción se habilita después de la creación de un proyecto).  
  
    Si previamente se ha conectado a SQL Server, el nombre del comando se volverá **a conectar a SQL Server**.  
  
2.  En el cuadro de diálogo conexión, escriba o seleccione el nombre de la instancia de SQL Server.  
  
    -   Si se está conectando a la instancia predeterminada en el equipo local, puede especificar **localhost** o un punto (**.**).  
  
    -   Si se va a conectar a la instancia predeterminada en otro equipo, escriba el nombre del equipo.  
  
    -   Si se va a conectar a una instancia con nombre en otro equipo, escriba el nombre del equipo seguido de una barra diagonal inversa y, a continuación, el nombre de la instancia, como MyServer\MyInstance.  
  
3.  Si la instancia de SQL Server está configurada para aceptar conexiones en un puerto no predeterminado, escriba el número de puerto que se utiliza para las conexiones de SQL Server en el cuadro **Puerto del servidor** . Para la instancia predeterminada de SQL Server, el número de puerto predeterminado es 1433. En el caso de las instancias con nombre, SSMA intentará obtener el número de puerto del servicio de SQL Server Browser.  
  
4.  En el cuadro **autenticación** , seleccione el tipo de autenticación que se utilizará para la conexión. Para usar la cuenta de Windows actual, seleccione **autenticación de Windows**. Para usar un inicio de sesión de SQL Server, seleccione autenticación de SQL Server y proporcione el nombre de inicio de sesión y la contraseña.  
  
5.  Para una conexión segura, se agregan dos controles, las casillas de verificación **cifrar conexión** y **TrustServerCertificate** . Solo cuando se activa **cifrar conexión** , la casilla **TrustServerCertificate** está visible. Cuando se activa la opción **cifrar conexión** (true) y **TrustServerCertificate** está desactivado (false), se validará el certificado SSL SQL Server. Validar el certificado de servidor es una parte del protocolo de enlace de SSL y asegurarse de que el servidor es el apropiado al que hay que conectarse. Para garantizar esto, se debe instalar un certificado en el lado cliente y en el lado servidor.  
  
6.  Haga clic en Conectar.  
  
**Mayor compatibilidad de versiones**  
  
Puede conectarse o volver a conectarse a versiones posteriores de SQL Server.  
  
1.  Podrá conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 cuando el proyecto creado sea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
2.  Podrá conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 cuando el proyecto creado sea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 pero no se le permita conectarse a las versiones anteriores, es decir, a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
3.  Podrá conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 cuando el proyecto creado sea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012.  
  
4.  Solo podrá conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 cuando el proyecto creado sea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014.  
  
5.  La compatibilidad con versiones posteriores no es válida para "SQL Azure".  
  
|TIPO de proyecto frente a versión del servidor de destino|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005<br /> (Versión: 9. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008<br /> (Versión: 10. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012<br />(Versión: 11. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014<br />(Versión: 12. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016<br />(Versión: 13. x)|SQL Azure|  
|-|-|-|-|-|-|-|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|Sí|Sí|Sí|Sí|Sí||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||Sí|Sí|Sí|Sí||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||Sí|Sí|Sí||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014||||Sí|Sí||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016|||||Sí||  
|SQL Azure||||||Sí|  
  
> [!IMPORTANT]  
> La conversión de los objetos de base de datos se realiza según el tipo de proyecto, pero no según la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conectada a. En el caso del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proyecto 2005, la conversión se realiza según [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005, aunque esté conectado a una versión posterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016).  
  
## <a name="synchronizing-sql-server-metadata"></a>Sincronizar metadatos de SQL Server  
Los metadatos acerca de SQL Server bases de datos no se actualizan automáticamente. Los metadatos de SQL Server explorador de metadatos es una instantánea de los metadatos cuando se conectó por primera vez a SQL Server, o la última vez que se actualizaron los metadatos manualmente. Puede actualizar manualmente los metadatos de todas las bases de datos o de cualquier base de datos o objeto de base de datos.  
  
**Para sincronizar los metadatos**  
  
1.  Asegúrese de que está conectado a SQL Server.  
  
2.  En SQL Server explorador de metadatos, active la casilla situada junto a la base de datos o el esquema de la base de datos que desea actualizar.  
  
    Por ejemplo, para actualizar los metadatos de todas las bases de datos, active la casilla situada junto a bases de datos.  
  
3.  Haga clic con el botón derecho en bases de datos o en el esquema de base de datos o de base de datos individual y seleccione **sincronizar con base de datos**.  
  
## <a name="next-step"></a>siguiente paso  
El siguiente paso de la migración depende de las necesidades del proyecto:  
  
-   Para personalizar la asignación entre esquemas de MySQL y bases de datos y esquemas de SQL Server, consulte [asignación de bases de datos de MySQL a esquemas de SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
-   Para personalizar las opciones de configuración de los proyectos, vea [establecer opciones de proyecto &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)  
  
-   Para personalizar la asignación de los tipos de datos de origen y de destino, consulte [asignación de tipos de datos de SQL Server y MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   Si no tiene que realizar ninguna de estas tareas, puede convertir las definiciones de objetos de base de datos de MySQL en SQL Server definiciones de objeto. Para obtener más información, vea [convertir las bases de datos MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>Consulte también  
[Migración de bases de datos de MySQL a SQL Server Azure SQL Database &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
