---
title: Conectarse a Sybase ASE (SybaseToSQL) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Connecting to Sybase ASE
ms.assetid: a45a2330-9175-4c9e-af38-ef920e350614
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4cbdcd08cc4186dd4fa6d7d8fcffebdfd1139799
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="connecting-to-sybase-ase-sybasetosql"></a>Conectarse a Sybase ASE (SybaseToSQL)
Migrar bases de datos de Sybase Adaptive Server Enterprise (ASE) a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure, debe conectarse al servidor adaptable que contiene las bases de datos que se van a migrar. Cuando se conecta, SSMA obtiene metadatos acerca de todas las bases de datos en el servidor adaptable y muestra los metadatos de la base de datos en el panel Explorador de metadatos de Sybase. SSMA almacena información sobre el servidor de base de datos, pero no almacena las contraseñas.  
  
La conexión a ASE permanece activa hasta que se cierra el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse a ASE si desea que una conexión activa con el servidor.  
  
Metadatos acerca del servidor adaptable no se actualizan automáticamente. En su lugar, si desea actualizar los metadatos en el Explorador de metadatos de Sybase, debe actualizar manualmente los metadatos, como se describe en la sección "Actualizar los metadatos de Sybase ASE" más adelante en este tema.  
  
## <a name="required-ase-permissions"></a>Permisos necesarios ASE  
La cuenta que se usa para conectarse a ASE debe tener al menos **público** acceso a la base de datos maestra y a las bases de datos de origen para migrarlos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure. Además, para seleccionar los permisos en las tablas que se van a migrar, el usuario debe tener permisos SELECT en las tablas del sistema siguientes:  
  
-   .dbo.sysobjects [source_db]  
  
-   .dbo.syscolumns [source_db]  
  
-   .dbo.sysusers [source_db]  
  
-   .dbo.systypes [source_db]  
  
-   .dbo.sysconstraints [source_db]  
  
-   .dbo.syscomments [source_db]  
  
-   .dbo.sysindexes [source_db]  
  
-   .dbo.sysreferences [source_db]  
  
-   master.dbo.sysdatabases  
  
## <a name="establishing-a-connection-to-ase"></a>Establecer una conexión con ASE  
Cuando se conecta a un servidor adaptable, SSMA lee los metadatos de la base de datos en el servidor de base de datos y, a continuación, agrega estos metadatos para el archivo de proyecto. SSMA utiliza estos metadatos cuando convierte los objetos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o la sintaxis de SQL Azure, y cuando migra los datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure. Puede examinar estos metadatos en el panel del explorador de metadatos de Sybase y revise las propiedades de objetos de base de datos individuales.  
  
> [!IMPORTANT]  
> Antes de intentar conectarse al servidor de base de datos, asegúrese de el servidor de base de datos se está ejecutando y puede aceptar conexiones.  
  
**Para conectarse a Sybase ASE**  
  
1.  En el **archivo** menú, seleccione **conectar para Sybase**.  
  
    Si se ha conectado anteriormente a Sybase, será el nombre del comando **conectarse de nuevo a Sybase**.  
  
2.  En el **proveedor** , seleccione cualquiera de los proveedores instalados en el equipo para conectarse al servidor de Sybase.  
  
3.  En el **modo** , seleccione **modo estándar** o **modo avanzado**.  
  
    Utilice el modo estándar para especificar el nombre del servidor, el puerto, el nombre de usuario y la contraseña. Usar modo avanzado para proporcionar una cadena de conexión. Este modo es normalmente sólo se utiliza para solucionar problemas o para trabajar con el soporte técnico.  
  
4.  Si selecciona **modo estándar**, proporcione los valores siguientes:  
  
    1.  En el **nombre del servidor** cuadro, escriba o seleccione el nombre o dirección IP del servidor de base de datos.  
  
    2.  Si el servidor de base de datos no está configurado para aceptar conexiones en el valor predeterminado (5000) de puerto, escriba el número de puerto que se utiliza para las conexiones de Sybase en el **puerto del servidor** cuadro.  
  
    3.  En el **nombre de usuario** cuadro, escriba una cuenta de Sybase que tenga los permisos necesarios.  
  
    4.  En el **contraseña** cuadro, escriba la contraseña para el nombre de usuario especificado.  
  
5.  Si selecciona **modo avanzado**, proporcionar una cadena de conexión en el **cadena de conexión** cuadro.  
  
    Ejemplos de cadenas de conexión diferentes son los siguientes:  
  
    1.  **Cadenas de conexión para el proveedor OLE DB de Sybase:**  
  
        Para Sybase ASE OLE DB 12,5, una cadena de conexión de ejemplo es la siguiente:  
  
        `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
        Para Sybase ASE OLE DB 15, una cadena de conexión de ejemplo es la siguiente:  
  
        `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider= ASEOLEDB;Port=5000;`  
  
    2.  **Cadena de conexión para el proveedor de Sybase ODBC:**  
  
        `Driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
    3.  **Cadena de conexión para el proveedor de ADO.NET de Sybase:**  
  
        `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
    Para obtener más información, vea [conectar para Sybase &#40; SybaseToSQL &#41; ](../../ssma/sybase/connect-to-sybase-sybasetosql.md).  
  
## <a name="reconnecting-to-sybase-ase"></a>Volver a conectarse para Sybase ASE  
La conexión con el servidor de base de datos permanece activa hasta que se cierra el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse si desea que una conexión activa con el servidor adaptable. Puede trabajar sin conexión hasta que desee actualizar los metadatos, cargar los objetos de base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure, y migrar los datos.  
  
## <a name="refreshing-sybase-ase-metadata"></a>Actualizar los metadatos de Sybase ASE  
No se actualizan automáticamente los metadatos acerca de las bases de datos de ASE. Los metadatos en el Explorador de metadatos de Sybase están una instantánea de los metadatos cuando se conectó por primera vez al servidor adaptable o la última vez que actualiza manualmente los metadatos. Puede actualizar manualmente los metadatos para una sola base de datos, un esquema de base de datos individual o todas las bases de datos.  
  
**Para actualizar los metadatos**  
  
1.  Asegúrese de que está conectado al servidor adaptable.  
  
2.  En el Explorador de metadatos de Sybase, active la casilla de verificación junto a la base de datos o el esquema de base de datos que desea actualizar.  
  
3.  Haga clic en las bases de datos o la base de datos individual o el esquema de base de datos y, a continuación, seleccione **actualizar desde la base de datos**.  
  
4.  Si le solicita que compruebe el objeto actual, haga clic en **Sí**.  
  
## <a name="next-step"></a>Paso siguiente  
  
-   El siguiente paso del proceso de migración consiste en [conecta a una instancia de SQL Server](http://msdn.microsoft.com/en-us/dd368a1a-45b0-40e9-b4d3-5cdb48c26606) / [conectarse a una instancia de SQL Azure](http://msdn.microsoft.com/en-us/9e77e4b0-40c0-455c-8431-ca5d43849aa7)  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de ASE de Sybase a SQL Server: base de datos de SQL Azure &#40; SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

