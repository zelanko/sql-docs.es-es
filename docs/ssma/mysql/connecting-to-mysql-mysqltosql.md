---
title: Conectar con MySQL (MySQLToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Connecting to MySQL, MySQL permission
- Connecting to MySQL,reconnecting
ms.assetid: 084c7020-f729-4f91-90e0-143f85fa68d1
caps.latest.revision: "13"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 18c53f8c1e8118fe1eb3cedcd12c7851c35ec10a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="connecting-to-mysql-mysqltosql"></a>Conectar con MySQL (MySQLToSQL)
Para migrar las bases de datos de MySQL a SQL Server o SQL Azure, debe conectarse a la base de datos de MySQL que se va a migrar. Cuando se conecta, SSMA obtiene metadatos acerca de todos los esquemas de MySQL y, a continuación, muestra en el panel Explorador de metadatos de MySQL. SSMA almacena información sobre el servidor de base de datos, pero no almacena las contraseñas.  
  
La conexión a la base de datos permanece activa hasta que se cierra el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse si desea que una conexión activa a la base de datos.  
  
Metadatos acerca de la base de datos MySQL no se actualizan automáticamente. En su lugar, si desea actualizar los metadatos en el Explorador de metadatos de MySQL, debe actualizarlo manualmente. Para obtener más información, vea la sección "Actualizar metadatos de MySQL" más adelante en este tema.  
  
## <a name="required-mysql-permissions"></a>Permisos necesarios de MySQL  
La cuenta que se usa para conectarse a la base de datos de MySQL debe tener al menos **conectar** permisos. Esto permite SSMA obtener los metadatos de esquemas propiedad de usuario que se conecta. Para obtener los metadatos para los objetos de otros esquemas y, a continuación, convertir objetos en los esquemas, la cuenta debe tener los permisos siguientes:  
  
-   Privilegios 'SHOW' en objetos de base de datos  
  
-   Privilegio 'SELECT' en 'Information_schema'  
  
-   Privilegio 'SELECT' en mysql (para UDF)  
  
## <a name="establishing-a-connection-to-mysql"></a>Establecer una conexión con MySQL  
Cuando se conecta a una base de datos, SSMA lee los metadatos de la base de datos y, a continuación, agrega estos metadatos para el archivo de proyecto. Estos metadatos se usan por SSMA cuando convierte los objetos en la sintaxis de SQL Server o SQL Azure, y cuando migra los datos a SQL Server o SQL Azure. Puede examinar estos metadatos en el panel del explorador de metadatos de MySQL y revise las propiedades de objetos de base de datos individuales.  
  
> [!IMPORTANT]  
> Antes de intentar conectarse, asegúrese de el servidor de base de datos se está ejecutando y puede aceptar conexiones.  
  
**Para conectarse a MySQL**  
  
1.  En el **archivo** menú, seleccione **conectar con MySQL** (esta opción se habilitarán después de la creación del proyecto).  
  
    Si se conectó a MySQL, será el nombre del comando **volver a conectar con MySQL**.  
  
2.  En el **proveedor** , seleccione el controlador de MySQL ODBC 5.1 (de confianza). Es el proveedor predeterminado en el modo estándar.  
  
3.  En el **modo** cuadro, seleccione **modo estándar**. Este es el modo predeterminado.  
  
    Utilice el modo estándar para especificar el nombre del servidor y el puerto.  
  
4.  En **modo estándar**, proporcione los valores siguientes:  
  
    1.  En el **nombre del servidor** cuadro, escriba el nombre del servidor MySQL. En el **puerto del servidor** cuadro, escriba el número de puerto para que sea 3306. Es el puerto predeterminado.  
  
    2.  En el **nombre de usuario** cuadro, escriba una cuenta de MySQL que tenga los permisos necesarios.  
  
    3.  En el **contraseña** cuadro, escriba la contraseña para el nombre de usuario especificado.  
  
5.  **SSL:** si desea conectarse de forma segura MySQL, asegúrese de utilizar capa de sockets seguros (SSL) al comprobar la **SSL** casilla de verificación.  
  
6.  **Configurar:** proporciona una opción para configurar la conexión de MySQL a través de la capa de sockets seguros (SSL).  
  
    > [!NOTE]  
    > Para habilitar **configurar**, SSL debe estar establecido en **True**.  
  
    Al hacer clic en el botón "Configurar", aparece un cuadro de diálogo. Para utilizar el cifrado al conectarse a la base de datos de MySQL, ruta de acceso a los siguientes archivos de tres certificado presentes en el cuadro de diálogo debe ser define [privacidad mejorada correo certificados (PEM)]:  
  
    -   **Entidad emisora de certificados SSL:** especifica la ruta de acceso a un archivo con una lista de confianza de entidades emisoras de certificados SSL.  
  
    -   **Certificado SSL:** especifica el nombre del archivo de certificado SSL que se utilizará para establecer una conexión segura.  
  
    -   **CLAVE de SSL:** especifica el nombre del archivo de clave de SSL que se utilizará para establecer una conexión segura.  
  
    > [!NOTE]  
    > -   El **Aceptar** botón se habilita cuando se ha proporcionado la información necesaria. Si cualquiera de las rutas de acceso de archivo son válido, el botón "Aceptar" permanecerá deshabilitado.  
    > -   El **cancelar** botón cierra el cuadro de diálogo y **desactiva** la opción SSL desde el formulario de conexión principal.  
  
7.  Para obtener más información, vea [conectar con MySQL &#40; MySQLToSQL &#41;](../../ssma/mysql/connect-to-mysql-mysqltosql.md)  
  
## <a name="reconnecting-to-mysql"></a>Volver a conectarse a MySQL  
La conexión con el servidor de base de datos permanece activa hasta que se cierra el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse si desea que una conexión activa a la base de datos. Puede trabajar sin conexión hasta que desee actualizar los metadatos, cargará los objetos de base de datos en SQL Server o SQL Azure y migrar los datos.  
  
## <a name="refreshing-mysql-metadata"></a>Actualizar los metadatos de MySQL  
No se actualizan automáticamente los metadatos acerca de la base de datos de MySQL. Los metadatos en el Explorador de metadatos de MySQL están una instantánea de los metadatos cuando conectó por primera vez, o la última vez que actualiza manualmente los metadatos. Puede actualizar manualmente los metadatos para todos los esquemas, un único esquema u objetos de base de datos individuales.  
  
**Para actualizar los metadatos**  
  
1.  Asegúrese de que está conectado a la base de datos.  
  
2.  En el Explorador de metadatos de MySQL, seleccione la casilla situada junto a cada objeto de esquema o base de datos que desea actualizar.  
  
3.  Haga clic en **esquemas**, o el esquema en particular o la base de datos de objeto y, a continuación, seleccione **actualizar desde la base de datos**.  
  
    Si no tiene una conexión activa, SSMA mostrará el **conectar con MySQL** cuadro de diálogo para que puedan conectarse.  
  
4.  En la actualización desde el cuadro de diálogo de la base de datos, especificar qué objetos desea actualizar.  
  
    -   Para actualizar un objeto, haga clic en el **Active** campo adyacente al objeto hasta que aparezca una flecha.  
  
    -   Para evitar que un objeto que se está actualizando, haga clic en el **Active** campo adyacente para el objeto hasta que un **X** aparece.  
  
    -   Para actualizar o rechazar una categoría de objetos, haga clic en el **Active** campo junto a la carpeta de la categoría.  
  
    -   Para ver las definiciones de la codificación de color, haga clic en el **leyenda** botón.  
  
5.  Haga clic en **Aceptar**.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso del proceso de migración es [conectarse a SQL Server &#40; MySQLToSQL &#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de MySQL a SQL Server: base de datos de SQL Azure &#40; MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
