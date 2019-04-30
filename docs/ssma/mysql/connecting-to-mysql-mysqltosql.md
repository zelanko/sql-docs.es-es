---
title: Conectar con MySQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to MySQL, MySQL permission
- Connecting to MySQL,reconnecting
ms.assetid: 084c7020-f729-4f91-90e0-143f85fa68d1
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 233b6824ef527a9ed4e7e02164a08e31e41f3699
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63253324"
---
# <a name="connecting-to-mysql-mysqltosql"></a>Conexión a MySQL (MySQLToSQL)
Para migrar bases de datos MySQL a SQL Server o SQL Azure, debe conectarse a la base de datos MySQL que se va a migrar. Cuando se conecta, SSMA obtiene metadatos sobre todos los esquemas de MySQL y, a continuación, muestra en el panel Explorador de metadatos de MySQL. SSMA almacena información sobre el servidor de base de datos, pero no almacena las contraseñas.  
  
La conexión a la base de datos permanece activa hasta que cierre el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse si desea que una conexión activa a la base de datos.  
  
Metadatos acerca de la base de datos MySQL no se actualizan automáticamente. En su lugar, si desea actualizar los metadatos en el Explorador de metadatos de MySQL, debe actualizarlo manualmente. Para obtener más información, consulte la sección "Actualizar metadatos de MySQL" más adelante en este tema.  
  
## <a name="required-mysql-permissions"></a>Permisos necesarios de MySQL  
La cuenta que se usa para conectarse a la base de datos MySQL debe tener al menos **CONNECT** permisos. Esto permite SSMA obtener los metadatos de los esquemas de usuario que se conecta. Para obtener los metadatos de objetos en otros esquemas y, a continuación, convertir objetos en los esquemas, la cuenta debe tener los permisos siguientes:  
  
-   Mostrar privilegios en objetos de base de datos  
  
-   Privilegio 'SELECT' en 'Information_schema'  
  
-   'SELECT' privilegio en mysql (para UDF)  
  
## <a name="establishing-a-connection-to-mysql"></a>Establecer una conexión a MySQL  
Cuando se conecta a una base de datos, SSMA lee los metadatos de la base de datos y, a continuación, agrega estos metadatos al archivo de proyecto. Estos metadatos se usan por SSMA cuando convierte objetos a la sintaxis de SQL Server o SQL Azure, y cuando migra los datos a SQL Server o SQL Azure. Puede examinar estos metadatos en el panel Explorador de metadatos de MySQL y revisar las propiedades de objetos de base de datos individual.  
  
> [!IMPORTANT]  
> Antes de intentar conectarse, asegúrese de que el servidor de base de datos se está ejecutando y puede aceptar conexiones.  
  
**Para conectarse a MySQL**  
  
1.  En el **archivo** menú, seleccione **conectar con MySQL** (esta opción se habilitará después de la creación del proyecto).  
  
    Si se conectó a MySQL, será el nombre del comando **volver a conectar con MySQL**.  
  
2.  En el **proveedor** , seleccione el controlador de 5.1 de ODBC de MySQL (de confianza). Es el proveedor predeterminado en el modo estándar.  
  
3.  En el **modo** cuadro, seleccione **modo estándar**. Este es el modo predeterminado.  
  
    Utilice el modo estándar para especificar el nombre del servidor y puerto.  
  
4.  En **modo estándar**, proporcione los valores siguientes:  
  
    1.  En el **nombre del servidor** , escriba el nombre del servidor MySQL. En el **puerto del servidor** , escriba el número de puerto para que sea 3306. Es el puerto predeterminado.  
  
    2.  En el **nombre de usuario** , escriba una cuenta de MySQL que tenga los permisos necesarios.  
  
    3.  En el **contraseña** , escriba la contraseña del nombre de usuario especificado.  
  
5.  **SSL:** Si desea conectarse de forma segura a MySQL, asegúrese de utilizar capa de sockets seguros (SSL) al comprobar la **SSL** casilla de verificación.  
  
6.  **Configurar:** Proporciona una opción para configurar la conexión a MySQL a través de la capa de sockets seguros (SSL).  
  
    > [!NOTE]  
    > Para habilitar **configurar**, SSL debe establecerse en **True**.  
  
    Al hacer clic en el botón "Configurar", aparece un cuadro de diálogo. Para usar el cifrado mientras se conecta a la base de datos MySQL, ruta de acceso a los siguientes archivos de tres certificado presentes en el cuadro de diálogo debe ser definido [privacidad mejorada correo certificados (PEM)]:  
  
    -   **Entidad emisora de certificados SSL:** Especifica la ruta de acceso a un archivo con una lista de confianza de entidades emisoras de certificados SSL.  
  
    -   **Certificado SSL:** Especifica el nombre del archivo de certificado SSL que se utilizará para establecer una conexión segura.  
  
    -   **CLAVE SSL:** Especifica el nombre del archivo de clave SSL que se utilizará para establecer una conexión segura.  
  
    > [!NOTE]  
    > -   El **Aceptar** botón se habilita cuando se ha proporcionado la información necesaria. Si cualquiera de las rutas de acceso de archivo son válida, el botón "Aceptar" permanecerá deshabilitado.  
    > -   El **cancelar** botón cierra el cuadro de diálogo y **desactiva** la opción SSL desde el formulario principal de la conexión.  
  
7.  Para obtener más información, consulte [conectar con MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connect-to-mysql-mysqltosql.md)  
  
## <a name="reconnecting-to-mysql"></a>Volver a conectarse a MySQL  
La conexión al servidor de base de datos permanece activa hasta que cierre el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse si desea que una conexión activa a la base de datos. Puede trabajar sin conexión hasta que desee actualizar los metadatos, cargará los objetos de base de datos en SQL Server o SQL Azure y migrar los datos.  
  
## <a name="refreshing-mysql-metadata"></a>Actualizar metadatos de MySQL  
Metadatos acerca de la base de datos MySQL no se actualizan automáticamente. Los metadatos en el Explorador de metadatos de MySQL están una instantánea de los metadatos cuando conectó en primer lugar, o la última vez que actualiza manualmente los metadatos. Puede actualizar manualmente los metadatos para todos los esquemas, un único esquema u objetos de base de datos individual.  
  
**Para actualizar los metadatos**  
  
1.  Asegúrese de que está conectado a la base de datos.  
  
2.  En el Explorador de metadatos de MySQL, seleccione la casilla de verificación junto a cada objeto de esquema o base de datos que desea actualizar.  
  
3.  Haga clic en **esquemas**, o el esquema en particular o la base de datos de objeto y, a continuación, seleccione **actualizar desde la base de datos**.  
  
    Si no tiene una conexión activa, SSMA mostrará el **conectar con MySQL** cuadro de diálogo para que pueda conectarse.  
  
4.  En la actualización desde el cuadro de diálogo de la base de datos, especificar qué objetos desea actualizar.  
  
    -   Para actualizar un objeto, haga clic en el **Active** campo junto al objeto hasta que aparezca una flecha.  
  
    -   Para evitar que un objeto que se va a actualizar, haga clic en el **Active** campo adyacente para el objeto hasta que un **X** aparece.  
  
    -   Para actualizar o rechazar una categoría de objetos, haga clic en el **Active** campo junto a la carpeta de la categoría.  
  
    -   Para ver las definiciones de la codificación en colores, haga clic en el **leyenda** botón.  
  
5.  Haga clic en **Aceptar**.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso del proceso de migración es [conectarse a SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
## <a name="see-also"></a>Vea también  
[Bases de datos de migración desde MySQL a SQL Server: base de datos SQL Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
