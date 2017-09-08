---
title: Conectarse a la base de datos de Oracle (OracleToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Refreshing Oracle Metadata
ms.assetid: e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b6a4ac43e0f79e8f7841f8f9d4234ccdd988a7b6
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="connecting-to-oracle-database-oracletosql"></a>Conectarse a la base de datos de Oracle (OracleToSQL)
Para migrar bases de datos de Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], debe conectarse a la base de datos de Oracle que se va a migrar. Cuando se conecta, SSMA obtiene metadatos acerca de todos los esquemas de Oracle y, a continuación, muestra en el panel Explorador de metadatos de Oracle. SSMA almacena información sobre el servidor de base de datos, pero no almacena las contraseñas.  
  
La conexión a la base de datos permanece activa hasta que se cierra el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse si desea que una conexión activa a la base de datos.  
  
Metadatos acerca de la base de datos de Oracle no se actualizan automáticamente. En su lugar, si desea actualizar los metadatos en el Explorador de metadatos de Oracle, debe actualizarlo manualmente. Para obtener más información, vea la sección "Actualizar metadatos de Oracle" más adelante en este tema.  
  
## <a name="required-oracle-permissions"></a>Permisos de Oracle necesarios  
La cuenta que se usa para conectarse a la base de datos de Oracle debe tener al menos **conectar** permisos. Esto permite SSMA obtener los metadatos de esquemas propiedad de usuario que se conecta. Para obtener los metadatos para los objetos de otros esquemas y, a continuación, convertir objetos en los esquemas, la cuenta debe tener los permisos siguientes:  
  
-   CREAR UN PROCEDIMIENTO  
  
-   EJECUTAR UN PROCEDIMIENTO  
  
-   SELECCIONE CUALQUIER TABLA  
  
-   SELECCIONE CUALQUIER SECUENCIA  
  
-   CREAR CUALQUIER TIPO  
  
-   CREAR CUALQUIER DESENCADENADOR  
  
-   SELECCIONAR CUALQUIER DICCIONARIO  
  
## <a name="establishing-a-connection-to-oracle"></a>Establecer una conexión a Oracle  
Cuando se conecta a una base de datos, SSMA lee los metadatos de la base de datos y, a continuación, agrega estos metadatos para el archivo de proyecto. SSMA utiliza estos metadatos cuando convierte los objetos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sintaxis, y cuando migra los datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Puede examinar estos metadatos en el panel del explorador de metadatos de Oracle y revise las propiedades de objetos de base de datos individuales.  
  
> [!IMPORTANT]  
> Antes de intentar conectarse, asegúrese de el servidor de base de datos se está ejecutando y puede aceptar conexiones.  
  
**Para conectar con Oracle**  
  
1.  En el **archivo** menú, seleccione **conectar con Oracle**.  
  
    Si ya ha conectado a Oracle, el nombre de comando será **volver a conectar con Oracle**.  
  
2.  En el **proveedor** cuadro, seleccione **proveedor de cliente de Oracle** o **proveedor OLE DB**, dependiendo de qué proveedor está instalado. El valor predeterminado es cliente de Oracle.  
  
3.  En el **modo** , seleccione **modo estándar**, **modo TNSNAME**, o **modo de cadena de conexión**.  
  
    Utilice el modo estándar para especificar el nombre del servidor y el puerto. Usa el modo del nombre de servicio para especificar el nombre del servicio Oracle manualmente. Usar modo de cadena de conexión para proporcionar una cadena de conexión completa.  
  
4.  Si selecciona **modo estándar**, proporcione los valores siguientes:  
  
    1.  En el **nombre del servidor** cuadro, escriba o seleccione el nombre o dirección IP del servidor de base de datos.  
  
    2.  Si el servidor de base de datos no está configurado para aceptar conexiones en el valor predeterminado (1521) de puerto, escriba el número de puerto que se utiliza para las conexiones de Oracle en el **puerto del servidor** cuadro.  
  
    3.  En el **SID de Oracle** cuadro, escriba el identificador del sistema.  
  
    4.  En el **nombre de usuario** cuadro, escriba una cuenta de Oracle que tiene los permisos necesarios.  
  
    5.  En el **contraseña** cuadro, escriba la contraseña para el nombre de usuario especificado.  
  
5.  Si selecciona **modo TNSNAME**, proporcione los valores siguientes:  
  
    1.  En el **conectar identificador** cuadro, escriba conectarse identificador (alias TNS) de la base de datos.  
  
    2.  En el **nombre de usuario** cuadro, escriba una cuenta de Oracle que tiene los permisos necesarios.  
  
    3.  En el **contraseña** cuadro, escriba la contraseña para el nombre de usuario especificado.  
  
6.  Si selecciona **modo de cadena de conexión**, proporcionar una cadena de conexión en el **cadena de conexión** cuadro.  
  
    En el ejemplo siguiente se muestra una cadena de conexión OLE DB:  
  
    `Provider=OraOLEDB.Oracle;Data Source=MyOracleDB;User Id=myUsername;Password=myPassword;`  
  
    En el ejemplo siguiente se muestra una cadena de conexión de cliente de Oracle que utiliza la seguridad integrada:  
  
    `Data Source=MyOracleDB;Integrated Security=yes;`  
  
    Para obtener más información, consulte [conectarse a Oracle &#40; OracleToSQL &#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md).  
  
## <a name="reconnecting-to-oracle"></a>Volver a conectarse a Oracle  
La conexión con el servidor de base de datos permanece activa hasta que se cierra el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse si desea que una conexión activa a la base de datos. Puede trabajar sin conexión hasta que desee actualizar los metadatos, cargar los objetos de base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], y migrar los datos.  
  
## <a name="refreshing-oracle-metadata"></a>Actualizar los metadatos de Oracle  
No se actualizan automáticamente los metadatos acerca de la base de datos de Oracle. Los metadatos en el Explorador de metadatos de Oracle están una instantánea de los metadatos cuando conectó por primera vez, o la última vez que actualiza manualmente los metadatos. Puede actualizar manualmente los metadatos para todos los esquemas, un único esquema u objetos de base de datos individuales.  
  
**Para actualizar los metadatos**  
  
1.  Asegúrese de que está conectado a la base de datos.  
  
2.  En el Explorador de metadatos de Oracle, active la casilla de verificación junto a cada objeto de esquema o base de datos que desea actualizar.  
  
3.  Haga clic en **esquemas**, o el esquema en particular o la base de datos de objeto y, a continuación, seleccione **actualizar desde la base de datos**.  
  
    Si no tiene una conexión activa, SSMA mostrará el **conectar con Oracle** cuadro de diálogo para que puedan conectarse.  
  
4.  En la actualización desde el cuadro de diálogo de la base de datos, especificar qué objetos desea actualizar.  
  
    -   Para actualizar un objeto, haga clic en el **Active** campo adyacente al objeto hasta que aparezca una flecha.  
  
    -   Para evitar que un objeto que se está actualizando, haga clic en el **Active** campo adyacente para el objeto hasta que un **X** aparece.  
  
    -   Para actualizar o rechazar una categoría de objetos, haga clic en el **Active** campo junto a la carpeta de la categoría.  
  
    Para ver las definiciones de la codificación de color, haga clic en el **leyenda** botón.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
## <a name="next-step"></a>Paso siguiente  
  
-   El siguiente paso del proceso de migración consiste en [conecta a una instancia de SQL Server](http://msdn.microsoft.com/en-us/1b2a8059-1829-4904-a82f-9c06de1e245f).  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Oracle a SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  

