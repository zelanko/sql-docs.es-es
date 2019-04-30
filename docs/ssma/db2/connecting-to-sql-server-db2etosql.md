---
title: Conectarse a SQL Server (DB2eToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: b59803cb-3cc6-41cc-8553-faf90851410e
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 26410a933c7432189f664c2b04d2b41e3e31c9c2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63298992"
---
# <a name="connecting-to-sql-server-db2etosql"></a>Conectarse a SQL Server (DB2eToSQL)
Para migrar bases de datos DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 o Azure SQL Database debe conectarse a cualquiera de estas instancias de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cuando se conecta, SSMA obtiene metadatos acerca de todas las bases de datos en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y muestra los metadatos de la base de datos en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Explorador de metadatos. SSMA almacena información acerca de qué instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están conectados a, pero no almacena las contraseñas.  
  
La conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permanece activa hasta que cierre el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si desea que una conexión activa con el servidor. Puede trabajar sin conexión hasta que se carga los objetos de base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y migrar los datos.  
  
Metadatos acerca de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se sincroniza automáticamente. En su lugar, para actualizar los metadatos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el Explorador de metadatos, debe actualizar manualmente el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadatos. Para obtener más información, consulte la "Synchronizing [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadatos" más adelante en este tema.  
  
## <a name="required-sql-server-permissions"></a>Permisos necesarios de SQL Server  
La cuenta que se usa para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requiere permisos distintos dependiendo de las acciones que realiza la cuenta:  
  
-   Para convertir objetos de DB2 a [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxis para actualizar los metadatos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o para guardar sintaxis convertidos en scripts, la cuenta debe tener permiso para iniciar sesión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Para cargar los objetos de base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la cuenta debe ser un miembro de la **sysadmin** rol de servidor. Esto es necesario para instalar a los ensamblados CLR.  
  
-   Para migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la cuenta debe ser un miembro de la **sysadmin** rol de servidor. Esto es necesario para ejecutar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] paquetes de migración de datos del agente.  
  
-   Para ejecutar el código generado por SSMA, la cuenta debe tener **Execute** permisos para todas las funciones definidas por el usuario en el **ssma_DB2** esquema de la base de datos de destino. Estas funciones proporcionan una funcionalidad equivalente de funciones del sistema de DB2 y utilizadas por los objetos convertidos.  
  
Si la cuenta que se usa para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es realizar la migración de todas las tareas, la cuenta debe ser un miembro de la **sysadmin** rol de servidor.  
  
## <a name="establishing-a-sql-server-connection"></a>Establecer una conexión con SQL Server  
Antes de convertir los objetos de base de datos DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxis, debe establecer una conexión a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] donde van a migrar la base de datos DB2 o bases de datos.  
  
Al definir las propiedades de conexión, también se especifique la base de datos donde se migrarán los objetos y datos. Puede personalizar esta asignación en el nivel de esquema DB2 después de conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, consulte [asignación de esquemas de DB2 a esquemas de SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-schemas-to-sql-server-schemas-db2tosql.md).  
  
> [!IMPORTANT]  
> Antes de intentar conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], asegúrese de que la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se está ejecutando y puede aceptar conexiones.  
  
**Para conectarse a SQL Server**  
  
1.  En el **archivo** menú, seleccione **conectar con SQL Server**.  
  
    Si se ha conectado anteriormente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], será el nombre del comando **volver a conectar a SQL Server**.  
  
2.  En el cuadro de diálogo de conexión, escriba o seleccione el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Si se conecta a la instancia predeterminada en el equipo local, puede escribir **localhost** o un punto (**.**).  
  
    -   Si se conecta a la instancia predeterminada en otro equipo, escriba el nombre del equipo.  
  
    -   Si se conecta a una instancia con nombre en otro equipo, escriba el nombre del equipo seguido por una barra diagonal inversa y, a continuación, el nombre de instancia, como MyServer\MyInstance.  
  
3.  Si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está configurado para aceptar conexiones en un puerto no predeterminado, escriba el número de puerto que se utiliza para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexiones en el **puerto del servidor** cuadro. Para la instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el número de puerto predeterminado es 1433. Las instancias con nombre, SSMA intentará obtener el número de puerto desde el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio Browser.  
  
4.  En el **base de datos** , escriba el nombre de la base de datos de destino.  
  
    Esta opción no está disponible cuando se vuelve a conectar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
5.  En el **autenticación** , seleccione el tipo de autenticación que se usará para la conexión. Para usar la cuenta de Windows actual, seleccione **Windows autenticación**. Para usar un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión, seleccione **autenticación de SQL Server**y, a continuación, proporcione el nombre de inicio de sesión y contraseña.  
  
6.  Para una conexión segura, se agregan dos controles, el **cifrar conexión** y **TrustServerCertificate** casillas de verificación. Solo cuando **cifrar conexión** está activada, el **TrustServerCertificate** casilla de verificación está visible. Cuando **cifrar conexión** está activada (true) y **TrustServerCertificate** está desactivada (false), validará el certificado SSL de SQL Server. Validar el certificado de servidor es una parte del protocolo de enlace de SSL y asegurarse de que el servidor es el apropiado al que hay que conectarse. Para asegurarse de esto, debe instalar un certificado en el lado cliente, así como en el servidor.  
  
7.  Haga clic en **Conectar**.  
  
**Mayor compatibilidad de versión**  
  
-   Podrá conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 una vez creado el proyecto de migración [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
-   Podrá conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 una vez creado el proyecto de migración [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 pero no podrá conectarse a las versiones inferiores, es decir, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
-   Podrá conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 cuando el proyecto creado es SQL Server 2012.  
  
||||||  
|-|-|-|-|-|  
|**TIPO frente a la versión de servidor de destino del proyecto**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 <br />(Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 <br />(Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 <br />(Version:13.x)|Azure SQL DB|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|Sí|Sí|Sí||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014||Sí|Sí||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014|||Sí||  
|Azure SQL DB||||Sí|  
  
> [!IMPORTANT]  
> Conversión de los objetos de base de datos se lleva a cabo según el tipo de proyecto, pero no según la versión de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están conectados a. En caso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 o Azure SQL Database.  
  
## <a name="synchronizing-sql-server-metadata"></a>Sincronizar los metadatos de SQL Server  
Los metadatos sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bases de datos no se actualiza automáticamente. Los metadatos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Explorador de metadatos es una instantánea de los metadatos cuando se conectó en primer lugar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o la última vez que se han actualizado manualmente los metadatos. Puede actualizar manualmente los metadatos para todas las bases de datos, o para cualquier base de datos única o un objeto de base de datos.  
  
**Para sincronizar los metadatos**  
  
1.  Asegúrese de que está conectado a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el Explorador de metadatos, active la casilla situada junto a la base de datos o esquema que desea actualizar la base de datos.  
  
    Por ejemplo, para actualizar los metadatos de todas las bases de datos, active la casilla junto a **bases de datos**.  
  
3.  Haga clic en **bases de datos**, o de la base de datos individual o esquema de base de datos y a continuación, seleccione **sincronizar con base de datos**.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso en la migración depende de las necesidades del proyecto:  
  
-   Para personalizar la asignación entre esquemas de DB2 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bases de datos y esquemas, vea [asignación de esquemas de DB2 a esquemas de SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-schemas-to-sql-server-schemas-db2tosql.md).  
  
-   Para personalizar las opciones de configuración para los proyectos, vea [configuración del proyecto &#40;conversión&#41; &#40;DB2ToSQL&#41; ](../../ssma/db2/project-settings-conversion-db2tosql.md) y secciones relacionadas.  
  
-   Para personalizar la asignación de tipos de datos de origen y destino, vea [asignación DB2 y tipos de datos de SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md).  
  
-   Si no es necesario realizar ninguna de estas tareas, puede convertir las definiciones de objeto de base de datos de DB2 en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definiciones de objetos. Para obtener más información, consulte [convertir esquemas de DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md).  
  
## <a name="see-also"></a>Vea también  
[Las bases de datos DB2 migrar a SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
