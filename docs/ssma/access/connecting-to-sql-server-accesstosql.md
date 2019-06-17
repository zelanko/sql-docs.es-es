---
title: Conectarse a SQL Server (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- authentication
- instance of SQL Server
- metadata, refreshing
- ports
- refreshing metadata
- spaces in database names
- special characters
- SQL Server
- SQL Server, connecting
- SQL Server, connecting to
- SQL Server, reconnecting
ms.assetid: f84cf007-ddf1-4396-a07c-3e0729abc769
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 0bedb8ba74d7965df34a102fb0d53a0cbdb248dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63139029"
---
# <a name="connecting-to-sql-server-accesstosql"></a>Conectarse a SQL Server (AccessToSQL)
Para migrar bases de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe conectarse a la instancia de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cuando se conecta, SSMA obtiene los metadatos sobre las bases de datos en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y muestra los metadatos de la base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Explorador de metadatos. SSMA almacena información acerca de qué instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que están conectados a, pero no almacena las contraseñas.  
  
La conexión a SQL Server permanece activa hasta que cierre el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse a SQL Server si desea que una conexión activa con el servidor. Puede trabajar sin conexión hasta que se cargará los objetos de base de datos en SQL Server y migrar los datos.  
  
Metadatos acerca de la instancia de SQL Server no se sincronizan automáticamente. En su lugar, para actualizar los metadatos en el Explorador de metadatos de SQL Server, debe actualizar manualmente los metadatos de SQL Server. Para obtener más información, consulte la sección "Sincronizar los metadatos de SQL Server" más adelante en este tema.  
  
## <a name="required-sql-server-permissions"></a>Permisos necesarios de SQL Server  
La cuenta que se usa para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requiere permisos distintos dependiendo de las acciones realizadas por esa cuenta.  
  
-   Para convertir objetos de acceso a [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxis para actualizar los metadatos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o para guardar sintaxis convertidos en scripts, la cuenta debe tener permiso para iniciar sesión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Para cargar los objetos de base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y para migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el requisito de permiso mínimo es la pertenencia a la **db_owner** rol de base de datos en la base de datos de destino.  
  
## <a name="establishing-a-sql-server-connection"></a>Establecer una conexión con SQL Server  
Antes de convertir objetos de base de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxis, debe establecer una conexión a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] donde van a migrar sus bases de datos.  
  
Al definir las propiedades de conexión, también se especifique la base de datos donde se migrarán los objetos y datos. Puede personalizar esta asignación en el nivel de base de datos de acceso después de conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, consulte [asignación de origen y las bases de datos de destino](mapping-source-and-target-databases-accesstosql.md).  
  
> [!IMPORTANT]  
> Antes de conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], asegúrese de que la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se está ejecutando y puede aceptar conexiones. Para obtener más información, consulte "conectarse a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motor de base de datos" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla.  
  
**Para conectarse a SQL Server**  
  
1.  En el **archivo** menú, seleccione **conectar con SQL Server**.  
  
    Si se ha conectado anteriormente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], será el nombre del comando **volver a conectar a SQL Server**.  
  
2.  En el **nombre del servidor** cuadro, escriba o seleccione el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Si se conecta a la instancia predeterminada en el equipo local, puede escribir **localhost** o un punto ( **.** ).  
  
    -   Si se conecta a la instancia predeterminada en otro equipo, escriba el nombre del equipo.  
  
    -   Si se conecta a una instancia con nombre, escriba el nombre del equipo, una barra diagonal inversa y el nombre de instancia. Por ejemplo: MyServer\MyInstance.  
  
    -   Para conectarse a una instancia de usuario activas de [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)], conectarse mediante canalizaciones con nombre de protocolo y especificando el nombre de canalización, como \\ \\.\pipe\sql\query. Para obtener más información, consulte el [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] documentación.  
  
3.  Si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está configurado para aceptar conexiones en un puerto no predeterminado, escriba el número de puerto que se utiliza para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexiones en el **puerto del servidor** cuadro. Para la instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el número de puerto predeterminado es 1433. Las instancias con nombre, SSMA intentará obtener el número de puerto desde el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio Browser.  
  
4.  En el **base de datos** , escriba el nombre de la base de datos de destino para la migración de datos y objetos.  
  
    Esta opción no está disponible al volver a conectarse [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    El nombre de la base de datos de destino no puede contener espacios ni caracteres especiales. Por ejemplo, puede migrar las bases de datos de acceso a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos denominada "abc". Pero no se pueden migrar las bases de datos de acceso a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos denominada "a b-c".  
  
    Puede personalizar esta asignación por base de datos después de conectarse. Para obtener más información, consulte [asignación de origen y las bases de datos de destino](mapping-source-and-target-databases-accesstosql.md)  
  
5.  En el **autenticación** menú de lista desplegable, seleccione el tipo de autenticación que se usará para la conexión. Para usar la cuenta de Windows actual, seleccione **Windows autenticación**. Para usar un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión, seleccione **autenticación de SQL Server**y, a continuación, proporcione un nombre de usuario y una contraseña.  
  
6.  Para una conexión segura, se agregan dos controles, **cifrar conexión** Checkbox y **TrustServerCertificate** casilla de verificación. Solo cuando **cifrar conexión** está activada la casilla de verificación **TrustServerCertificate** casilla de verificación está visible. Cuando **cifrar conexión** es checked(true) y **TrustServerCertificate** es unchecked(false), validará el certificado SSL de SQL Server. Validar el certificado de servidor es una parte del protocolo de enlace de SSL y asegurarse de que el servidor es el apropiado al que hay que conectarse. Para asegurarse de esto, debe instalar un certificado en el lado cliente, así como en el servidor.  
  
7.  Haga clic en **Conectar**.  
  
**Mayor compatibilidad de versiones**  
  
Se puede conectar o volver a conectarse a versiones posteriores de SQL Server.  
  
1.  Podrá conectarse a SQL Server 2008 o SQL Server 2012, cuando el proyecto creado es SQL Server 2005.  
  
2.  Podrá conectarse a SQL Server 2012, cuando el proyecto creado es SQL Server 2008, pero no se permite para conectarse a las versiones inferiores, es decir, SQL Server 2005.  
  
3.  Podrá conectarse a solo SQL Server 2012, cuando el proyecto creado es SQL Server 2012.  
  
4.  Mayor compatibilidad de versión no es válido para SQL Azure.  
  
||||||||
|-|-|-|-|-|-|-|
|**TIPO frente a la versión de servidor de destino del proyecto**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 (versión: 9.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 (versión: 10.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 (Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 (Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 (Version:13.x)|SQL Azure|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|Sí|Sí|Sí|Sí|Sí||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||Sí|Sí|Sí|Sí||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||Sí|Sí|Sí||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014||||Sí|Sí||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|||||Sí||
|SQL Azure||||||Sí|
  
> [!IMPORTANT]  
> Conversión de los objetos de base de datos se lleva a cabo según el tipo de proyecto, pero no según la versión de SQL Server conectado a. Proyecto de SQL Server 2005, en el caso de conversión se lleva a cabo según SQL Server 2005, aunque están conectados a una versión posterior de SQL Server (SQL Server 2008/SQL/SQL Server 2012 Server 2014 o SQL Server 2016).  
  
## <a name="synchronizing-sql-server-metadata"></a>Sincronizar los metadatos de SQL Server  
Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los esquemas cambian después de conectarse, puede sincronizar los metadatos con el servidor.  
  
**Para sincronizar los metadatos de SQL Server**  
  
-   En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Explorador de metadatos, haga clic derecho **bases de datos**y, a continuación, seleccione **sincronizar con base de datos**.  
  
## <a name="reconnecting-to-sql-server"></a>Volver a conectarse a SQL Server  
La conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permanece activa hasta que cierre el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si desea que una conexión activa con el servidor. Puede trabajar sin conexión hasta que se carga los objetos de base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y migrar los datos.  
  
El procedimiento para volver a conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es el mismo que el procedimiento para establecer una conexión.  
  
## <a name="next-steps"></a>Pasos siguientes  
Si desea personalizar la asignación entre las bases de datos de origen y destino, consulte [bases de datos de destino y origen de asignación](mapping-source-and-target-databases-accesstosql.md) en caso contrario, es el siguiente paso convertir objetos de base de datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando sintaxis [convertir objetos de base de datos](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
