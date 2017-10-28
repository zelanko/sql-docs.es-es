---
title: Conectarse a la base de datos de DB2 (DB2ToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 5eb5801d-f0c3-4127-97c0-0b1ef49f4844
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3c7d7f8162968d579f1e3e1346fb2498ebf941cb
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="connecting-to-db2-database-db2tosql"></a>Conectarse a la base de datos de DB2 (DB2ToSQL)
Para migrar bases de datos de DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], debe conectarse a la base de datos de DB2 que se va a migrar. Cuando se conecta, SSMA obtiene metadatos acerca de todos los esquemas de DB2 y, a continuación, muestra en el panel Explorador de metadatos de DB2. SSMA almacena información sobre el servidor de base de datos, pero no almacena las contraseñas.  
  
La conexión a la base de datos permanece activa hasta que se cierra el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse si desea que una conexión activa a la base de datos.  
  
Metadatos acerca de la base de datos DB2 no se actualizan automáticamente. En su lugar, si desea actualizar los metadatos en el Explorador de metadatos de DB2, debe actualizarlo manualmente. Para obtener más información, vea la sección "Actualizar metadatos de DB2" más adelante en este tema.  
  
## <a name="required-db2-permissions"></a>Permisos necesarios de DB2  
Autorización de usuario define la lista de los comandos y los objetos que están disponibles para un usuario. Esta lista, por tanto, controla las acciones del usuario. En DB2, hay grupos predeterminados de privilegios para la autorización, en el nivel de instancia y en el nivel de base de datos DB2. Esto permite SSMA obtener los metadatos de esquemas propiedad de usuario que se conecta. Para obtener los metadatos para los objetos de otros esquemas y, a continuación, convertir objetos en los esquemas, la cuenta debe tener los permisos siguientes:  
  
-   Acceso de esquema para la migración de esquema normalmente se concede a PUBLIC, a menos que se usó la palabra clave restringir en crear  
  
-   Acceso a los datos para la migración de datos requiere DATAACCESS  
  
## <a name="establishing-a-connection-to-db2"></a>Establecer una conexión a DB2  
Cuando se conecta a una base de datos, SSMA lee los metadatos de la base de datos y, a continuación, agrega estos metadatos para el archivo de proyecto. SSMA utiliza estos metadatos cuando convierte los objetos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sintaxis, y cuando migra los datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Puede examinar estos metadatos en el panel del explorador de metadatos de DB2 y revise las propiedades de objetos de base de datos individuales.  
  
> [!IMPORTANT]  
> Antes de intentar conectarse, asegúrese de el servidor de base de datos se está ejecutando y puede aceptar conexiones.  
  
**Para conectarse a DB2**  
  
1.  En el **archivo** menú, seleccione **conectar a DB2**.  
  
    Si se ha conectado anteriormente a DB2, será el nombre del comando **volver a conectar a DB2**.  
  
2.  En el **proveedor** cuadro verá el **proveedor OLE DB** que actualmente es el único proveedor de acceso de cliente de DB2.  
  
3.  En el **Manager** cuadro puede seleccionar **Db2 para zOs**, o **DB2 para LUW**  
  
4.  En el **modo** , seleccione **modo estándar**, o **modo de cadena de conexión**.  
  
    Utilice el modo estándar para especificar el nombre del servidor y el puerto. Usa el modo del nombre de servicio para especificar el nombre del servicio DB2 manualmente. Usar modo de cadena de conexión para proporcionar una cadena de conexión completa.  
  
5.  Si selecciona **modo estándar**, proporcione los valores siguientes:  
  
    -   En el **nombre del servidor** cuadro, escriba o seleccione el nombre o dirección IP del servidor de base de datos.  
  
    -   Si el servidor de base de datos no está configurado para aceptar conexiones en el valor predeterminado (1521) de puerto, escriba el número de puerto que se utiliza para las conexiones de DB2 en el **puerto del servidor** cuadro.  
  
    -   En el **puerto del servidor** cuadro, escriba el número de puerto TCP/IP.  
  
    -   En el **Initial Catalog** cuadro, escriba el nombre de la base de datos  
  
    -   En el **nombre de usuario** cuadro, escriba una cuenta de DB2 que tenga los permisos necesarios.  
  
    -   En el **contraseña** cuadro, escriba la contraseña para el nombre de usuario especificado.  
  
6.  Si selecciona **modo de cadena de conexión**, proporcionar una cadena de conexión en el **cadena de conexión** cuadro.  
  
    En el ejemplo siguiente se muestra una cadena de conexión OLE DB:  
  
    `Provider=OraOLEDB.DB2;Data Source=MyDB2DB;User Id=myUsername;Password=myPassword;`  
  
    En el ejemplo siguiente se muestra una cadena de conexión de cliente de DB2 que utiliza la seguridad integrada:  
  
    `Data Source=MyDB2DB;Integrated Security=yes;`  
  
    Para obtener más información, consulte [conectarse a Oracle &#40; OracleToSQL &#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md).  
  
## <a name="reconnecting-to-db2"></a>Volver a conectar a DB2  
La conexión con el servidor de base de datos permanece activa hasta que se cierra el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse si desea que una conexión activa a la base de datos. Puede trabajar sin conexión hasta que desee actualizar los metadatos, cargar los objetos de base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], y migrar los datos.  
  
## <a name="refreshing-db2-metadata"></a>Actualizar los metadatos de DB2  
No se actualizan automáticamente los metadatos acerca de la base de datos DB2. Los metadatos en el Explorador de metadatos de DB2 están una instantánea de los metadatos cuando conectó por primera vez, o la última vez que actualiza manualmente los metadatos. Puede actualizar manualmente los metadatos para todos los esquemas, un único esquema u objetos de base de datos individuales.  
  
**Para actualizar los metadatos**  
  
1.  Asegúrese de que está conectado a la base de datos.  
  
2.  En el Explorador de metadatos de DB2, active la casilla de verificación junto a cada objeto de esquema o base de datos que desea actualizar.  
  
3.  Haga clic en **esquemas**, o el esquema en particular o la base de datos de objeto y, a continuación, seleccione **actualizar desde la base de datos**.  
  
    Si no tiene una conexión activa, SSMA mostrará el **conectar a DB2** cuadro de diálogo para que puedan conectarse.  
  
4.  En la actualización desde el cuadro de diálogo de la base de datos, especificar qué objetos desea actualizar.  
  
    -   Para actualizar un objeto, haga clic en el **Active** campo adyacente al objeto hasta que aparezca una flecha.  
  
    -   Para evitar que un objeto que se está actualizando, haga clic en el **Active** campo adyacente para el objeto hasta que un **X** aparece.  
  
    -   Para actualizar o rechazar una categoría de objetos, haga clic en el **Active** campo junto a la carpeta de la categoría.  
  
    Para ver las definiciones de la codificación de color, haga clic en el **leyenda** botón.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
## <a name="next-step"></a>Paso siguiente  
  
-   El siguiente paso del proceso de migración consiste en [conectarse a SQL Server](http://msdn.microsoft.com/en-us/b59803cb-3cc6-41cc-8553-faf90851410e).  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de DB2 a SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  

