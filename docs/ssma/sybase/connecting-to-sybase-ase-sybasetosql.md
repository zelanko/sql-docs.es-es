---
title: Conexión a Sybase ASE (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to Sybase ASE
ms.assetid: a45a2330-9175-4c9e-af38-ef920e350614
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d9c76a33a650284fde21b28af3a61b197829ef98
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63298541"
---
# <a name="connecting-to-sybase-ase-sybasetosql"></a>Conexión a Sybase ASE (SybaseToSQL)
Para migrar bases de datos de Sybase Adaptive Server Enterprise (ASE) a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, debe conectarse al servidor adaptable que contiene las bases de datos que desea migrar. Cuando se conecta, SSMA obtiene metadatos sobre todas las bases de datos en el servidor adaptable y muestra los metadatos de la base de datos en el panel Explorador de metadatos de Sybase. SSMA almacena información sobre el servidor de base de datos, pero no almacena las contraseñas.  
  
La conexión al ASE permanece activa hasta que cierre el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectar al ASE si desea que una conexión activa con el servidor.  
  
Los metadatos del servidor adaptable no se actualizan automáticamente. En su lugar, si desea actualizar los metadatos en el Explorador de metadatos de Sybase, debe actualizar manualmente los metadatos, como se describe en la sección "Actualizar los metadatos de Sybase ASE" más adelante en este tema.  
  
## <a name="required-ase-permissions"></a>Permisos necesarios de ASE  
La cuenta que se usa para conectarse a la instancia de ASE debe tener al menos **pública** acceso a la base de datos maestra y a las bases de datos de origen para migrarlos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Además, para seleccionar los permisos en las tablas que se van a migrar, el usuario debe tener permisos SELECT en las tablas del sistema siguientes:  
  
-   [source_db].dbo.sysobjects  
  
-   [source_db].dbo.syscolumns  
  
-   [source_db].dbo.sysusers  
  
-   [source_db].dbo.systypes  
  
-   [source_db].dbo.sysconstraints  
  
-   [source_db].dbo.syscomments  
  
-   [source_db].dbo.sysindexes  
  
-   [source_db].dbo.sysreferences  
  
-   master.dbo.sysdatabases  
  
## <a name="establishing-a-connection-to-ase"></a>Establecer una conexión a la instancia de ASE  
Cuando se conecta a un servidor adaptable, SSMA lee los metadatos de la base de datos en el servidor de base de datos y, a continuación, agrega estos metadatos al archivo de proyecto. SSMA utiliza estos metadatos al que convierte los objetos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o sintaxis de SQL Azure, y cuando migra los datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Puede examinar estos metadatos en el panel Explorador de metadatos de Sybase y revisar las propiedades de objetos de base de datos individual.  
  
> [!IMPORTANT]  
> Antes de intentar conectarse al servidor de base de datos, asegúrese de que el servidor de base de datos se está ejecutando y puede aceptar conexiones.  
  
**Para conectarse a Sybase ASE**  
  
1.  En el **archivo** menú, seleccione **conectarse a Sybase**.  
  
    Si se ha conectado anteriormente a Sybase, será el nombre del comando **volver a conectar a Sybase**.  
  
2.  En el **proveedor** , seleccione cualquiera de los proveedores instalados en el equipo para conectarse al servidor de Sybase.  
  
3.  En el **modo** , seleccione **modo estándar** o **modo avanzado**.  
  
    Utilice el modo estándar para especificar el nombre del servidor, puerto, nombre de usuario y contraseña. Use el modo avanzado para proporcionar una cadena de conexión. Este modo es normalmente solo se usa para solucionar problemas o para trabajar con el soporte técnico.  
  
4.  Si selecciona **modo estándar**, proporcione los valores siguientes:  
  
    1.  En el **nombre del servidor** cuadro, escriba o seleccione el nombre o dirección IP del servidor de base de datos.  
  
    2.  Si el servidor de base de datos no está configurado para aceptar conexiones en el valor predeterminado de puerto (5000), escriba el número de puerto que se usa para las conexiones de Sybase en el **puerto del servidor** cuadro.  
  
    3.  En el **nombre de usuario** , escriba una cuenta de Sybase que tenga los permisos necesarios.  
  
    4.  En el **contraseña** , escriba la contraseña del nombre de usuario especificado.  
  
5.  Si selecciona **modo avanzado**, proporcionar una cadena de conexión en el **cadena de conexión** cuadro.  
  
    Ejemplos de cadenas de conexión diferentes son los siguientes:  
  
    1.  **Cadenas de conexión para el proveedor OLE DB de Sybase:**  
  
        Para Sybase ASE OLE DB 12,5, una cadena de conexión de ejemplo es el siguiente:  
  
        `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
        Para Sybase ASE OLE DB 15, una cadena de conexión de ejemplo es el siguiente:  
  
        `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider= ASEOLEDB;Port=5000;`  
  
    2.  **Cadena de conexión para el proveedor ODBC de Sybase:**  
  
        `Driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
    3.  **Cadena de conexión para el proveedor de ADO.NET de Sybase:**  
  
        `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
    Para obtener más información, consulte [conectarse a Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/connect-to-sybase-sybasetosql.md).  
  
## <a name="reconnecting-to-sybase-ase"></a>Volver a conectarse a Sybase ASE  
La conexión al servidor de base de datos permanece activa hasta que cierre el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse si desea que una conexión activa con el servidor adaptable. Puede trabajar sin conexión hasta que desee actualizar los metadatos, cargar los objetos de base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, y migrar los datos.  
  
## <a name="refreshing-sybase-ase-metadata"></a>Actualizar metadatos de Sybase ASE  
Metadatos acerca de las bases de datos de ASE no se actualizan automáticamente. Los metadatos en el Explorador de metadatos de Sybase están una instantánea de los metadatos cuando se conectó en primer lugar en el servidor adaptable, o la última vez que actualiza manualmente los metadatos. Puede actualizar manualmente los metadatos de una sola base de datos, un esquema de base de datos única o todas las bases de datos.  
  
**Para actualizar los metadatos**  
  
1.  Asegúrese de que está conectado al servidor adaptable.  
  
2.  En el Explorador de metadatos de Sybase, active la casilla de verificación junto a la base de datos o esquema de base de datos que desea actualizar.  
  
3.  Haga clic en bases de datos o la base de datos individual o el esquema de base de datos y, a continuación, seleccione **actualizar desde la base de datos**.  
  
4.  Si se le pide que compruebe el objeto actual, haga clic en **Sí**.  
  
## <a name="next-step"></a>Paso siguiente  
  
-   El siguiente paso del proceso de migración es [conecta a una instancia de SQL Server](connecting-to-sql-server-sybasetosql.md) / [conectarse a una instancia de SQL Azure](connecting-to-azure-sql-db-sybasetosql.md)  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Sybase ASE a SQL Server: base de datos SQL Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
