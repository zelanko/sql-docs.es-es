---
title: Conexión a SQL Server (AccessToSQL) | Microsoft Docs
description: Obtenga información sobre cómo conectarse a una instancia de destino de SQL Database para migrar bases de datos de Access. SSMA obtiene metadatos acerca de las bases de datos en SQL Database.
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
ms.openlocfilehash: 6266eb0596b351a7ef54baed6a7a76a7a655ac60
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293102"
---
# <a name="connecting-to-sql-server-accesstosql"></a>Conexión a SQL Server (AccessToSQL)
Para migrar bases de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe conectarse a la instancia de de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Cuando se conecta, SSMA obtiene los metadatos de las bases de datos en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y muestra los metadatos de la base de datos en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Explorador de metadatos. SSMA almacena información acerca de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la que está conectado, pero no almacena contraseñas.  
  
La conexión a SQL Server permanece activa hasta que se cierra el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse a SQL Server si desea una conexión activa con el servidor. Puede trabajar sin conexión hasta que cargue los objetos de base de datos en SQL Server y migre los datos.  
  
Los metadatos sobre la instancia de SQL Server no se sincronizan automáticamente. En su lugar, para actualizar los metadatos en SQL Server explorador de metadatos, debe actualizar manualmente los metadatos de SQL Server. Para obtener más información, vea la sección "sincronizar metadatos de SQL Server" más adelante en este tema.  
  
## <a name="required-sql-server-permissions"></a>Permisos SQL Server necesarios  
La cuenta que se usa para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requiere permisos diferentes en función de las acciones realizadas por esa cuenta.  
  
-   Para convertir objetos de Access en [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxis, actualizar metadatos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o guardar la sintaxis convertida en scripts, la cuenta debe tener permiso para iniciar sesión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Para cargar los objetos de base de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos en y migrar los datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el requisito de permiso mínimo es la pertenencia al rol de base de datos **db_owner** en la base de datos de destino.  
  
## <a name="establishing-a-sql-server-connection"></a>Establecer una conexión SQL Server  
Antes de convertir los objetos de base [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de datos de Access a la sintaxis de, debe establecer una conexión con la instancia de en la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que desea migrar las bases de datos de Access.  
  
Al definir las propiedades de conexión, también se especifica la base de datos en la que se migrarán los objetos y los datos. Puede personalizar esta asignación en el nivel de base de datos de Access después de conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, vea [asignación de bases de datos de origen y de destino](mapping-source-and-target-databases-accesstosql.md).  
  
> [!IMPORTANT]  
> Antes de conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , asegúrese de que la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se está ejecutando y puede aceptar conexiones. Para obtener más información, vea "conectar con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motor de base de datos" en los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla de.  
  
**Para conectarse a SQL Server**  
  
1.  En el menú **archivo** , seleccione **conectarse a SQL Server**.  
  
    Si anteriormente se conectó a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el nombre del comando se volverá **a conectar a SQL Server**.  
  
2.  En el cuadro **nombre del servidor** , escriba o seleccione el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    -   Si se está conectando a la instancia predeterminada en el equipo local, puede especificar **localhost** o un punto (**.**).  
  
    -   Si se va a conectar a la instancia predeterminada en otro equipo, escriba el nombre del equipo.  
  
    -   Si se va a conectar a una instancia con nombre, escriba el nombre del equipo, una barra diagonal inversa y el nombre de la instancia. Por ejemplo: MyServer\MyInstance.  
  
    -   Para conectarse a una instancia de usuario activa de [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] , conéctese mediante el protocolo de canalizaciones con nombre y especifique el nombre de la canalización, como \\ \\ .\pipe\sql\query. Para obtener más información, consulte la documentación de [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] .  
  
3.  Si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está configurada para aceptar conexiones en un puerto no predeterminado, escriba el número de puerto que se utiliza para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] las conexiones en el cuadro **Puerto del servidor** . Para la instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el número de puerto predeterminado es 1433. En el caso de las instancias con nombre, SSMA intentará obtener el número de puerto del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio explorador.  
  
4.  En el cuadro **base** de datos, escriba el nombre de la base de datos de destino para la migración de datos y objetos.  
  
    Esta opción no está disponible cuando se vuelve a conectar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    El nombre de la base de datos de destino no puede contener espacios ni caracteres especiales. Por ejemplo, puede migrar las bases de datos de Access a una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos denominada "ABC". Sin embargo, no puede migrar las bases de datos de Access a una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos denominada "a b-c".  
  
    Puede personalizar esta asignación por base de datos después de conectarse. Para obtener más información, consulte [asignación de bases de datos de origen y de destino](mapping-source-and-target-databases-accesstosql.md) .  
  
5.  En el menú desplegable **autenticación** , seleccione el tipo de autenticación que se utilizará para la conexión. Para usar la cuenta de Windows actual, seleccione **autenticación de Windows**. Para usar un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Inicio de sesión, seleccione **SQL Server autenticación**y proporcione un nombre de usuario y una contraseña.  
  
6.  Para una conexión segura, se agregan dos controles, la casilla **cifrar conexión** y la casilla **TrustServerCertificate** . Solo cuando la casilla **cifrar conexión** está activada la casilla de verificación **TrustServerCertificate** está visible. Cuando se activa la opción **cifrar conexión** (true) y **TrustServerCertificate** está desactivado (false), validará el certificado SSL SQL Server. Validar el certificado de servidor es una parte del protocolo de enlace de SSL y asegurarse de que el servidor es el apropiado al que hay que conectarse. Para garantizar esto, se debe instalar un certificado en el lado cliente y en el lado servidor.  
  
7.  Haga clic en **Conectar**.  
  
**Mayor compatibilidad de versiones**  
  
Puede conectarse o volver a conectarse a versiones posteriores de SQL Server.  
  
1.  Podrá conectarse a SQL Server 2008 o SQL Server 2012 cuando el proyecto creado esté SQL Server 2005.  
  
2.  Podrá conectarse a SQL Server 2012 cuando el proyecto creado sea SQL Server 2008, pero no se le permitirá conectarse a las versiones anteriores, es decir, SQL Server 2005.  
  
3.  Solo podrá conectarse a SQL Server 2012 cuando el proyecto creado sea SQL Server 2012.  
  
4.  La compatibilidad con versiones posteriores no es válida para SQL Azure.  
  
||||||||
|-|-|-|-|-|-|-|
|**VERSIÓN de tipo de proyecto frente al servidor de destino**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005 (versión: 9. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008 (versión: 10. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012 (versión: 11. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 (versión: 12. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016 (versión: 13. x)|SQL Azure|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|Sí|Sí|Sí|Sí|Sí||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||Sí|Sí|Sí|Sí||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||Sí|Sí|Sí||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014||||Sí|Sí||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|||||Sí||
|SQL Azure||||||Sí|
  
> [!IMPORTANT]  
> La conversión de los objetos de base de datos se realiza según el tipo de proyecto, pero no según la versión de la SQL Server conectada a. En el caso de SQL Server proyecto 2005, la conversión se realiza según SQL Server 2005 aunque esté conectado a una versión posterior de SQL Server (SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016).  
  
## <a name="synchronizing-sql-server-metadata"></a>Sincronizar metadatos de SQL Server  
Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los esquemas cambian después de conectarse, puede sincronizar los metadatos con el servidor de.  
  
**Para sincronizar metadatos de SQL Server**  
  
-   En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el explorador de metadatos, haga clic con el botón derecho en **bases**de datos y seleccione **sincronizar con base de**datos.  
  
## <a name="reconnecting-to-sql-server"></a>Volver a conectar a SQL Server  
La conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permanece activa hasta que se cierra el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si desea una conexión activa con el servidor. Puede trabajar sin conexión hasta que cargue los objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de base de datos en y migre los datos.  
  
El procedimiento para volver a conectar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es el mismo que el procedimiento para establecer una conexión.  
  
## <a name="next-steps"></a>Pasos siguientes  
Si desea personalizar la asignación entre las bases de datos de origen y de destino, consulte [asignación de bases de datos de origen y de destino](mapping-source-and-target-databases-accesstosql.md) ; en caso contrario, el siguiente paso consiste en convertir los objetos de base de datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxis mediante la conversión de objetos de base de [datos](converting-access-database-objects-accesstosql.md) .  
  
## <a name="see-also"></a>Consulte también  
[Migrar bases de datos de Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
