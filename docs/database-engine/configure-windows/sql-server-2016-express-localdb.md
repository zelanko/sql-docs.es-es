---
title: SQL Server 2016 Express LocalDB | Microsoft Docs
ms.custom: 
ms.date: 08/10/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- user instances
- LocalDB, described
- local database runtime
- file database
- LocalDB
ms.assetid: 5a641a46-7cfb-4d7b-a90d-6e4625719d74
caps.latest.revision: 42
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 64d008b25aacd5ad76b711662f9b6ffd3e5e5926
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="sql-server-2016-express-localdb"></a>SQL Server 2016 Express LocalDB

 > Para obtener contenido relacionado con versiones anteriores de SQL Server, vea [SQL Server 2014 Express LocalDB](https://msdn.microsoft.com/en-US/library/hh510202(SQL.120).aspx).

Microsoft SQL Server 2016 Express **LocalDB** es una característica de [SQL Server Express](https://msdn.microsoft.com/library/ms144275(SQL.130).aspx) dirigida a los desarrolladores. Está disponible en SQL Server 2016 Express con Advanced Services.  

 La instalación de**LocalDB** copia un conjunto de archivos mínimo necesario para iniciar el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Una vez que LocalDB está instalado, puede iniciar una conexión mediante una cadena de conexión especial. Cuando se realiza la conexión, se crea y se inicia automáticamente la infraestructura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] necesaria, permitiendo que la aplicación use la base de datos sin tareas de configuración complejas. Las herramientas de desarrollo pueden proporcionar a los desarrolladores de software un [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que les permite escribir y probar el código de [!INCLUDE[tsql](../../includes/tsql-md.md)] sin tener que administrar una instancia de servidor completa de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
 
 
 ## <a name="try-it-out"></a>Pruébelo. 
  
-   Para descargar e instalar SQL Server 2016 Express, vaya a las **[descargas de SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)**. LocalDB es una característica que se selecciona durante la instalación y está disponible al descargar los medios. Si descarga los medios, elija **Express Advanced** o el paquete de **LocalDB** . 
  
-   ¿Tiene una cuenta de Azure?  Si es así, haga clic **[aquí](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/)** para poner en marcha una máquina virtual con [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ya instalado.  
  
## <a name="install-localdb"></a>Instalar LocalDB  
 Instale **LocalDB** mediante el asistente para la instalación o mediante el programa SqlLocalDB.msi. **LocalDB** es una opción cuando se instala [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)]. 
 
Seleccione **LocalDB** en la página **Selección de características/Características compartidas** durante la instalación. Solo puede haber una instalación de los archivos binarios de **LocalDB** para cada versión principal de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . Se pueden iniciar varios procesos de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y todos usarán los mismos binarios. Una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] iniciada como **LocalDB** tiene las mismas limitaciones que [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]  

 Una instancia de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] **LocalDB** se administra con la utilidad **SqlLocalDB.exe** . [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] **LocalDB** en lugar de la característica de instancia de usuario de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] , que ha quedado obsoleta. 
  
## <a name="description"></a>Descripción  
 El programa de instalación de **LocalDB** usa el programa SqlLocalDB.msi para instalar los archivos necesarios en el equipo. Una vez instalado, **LocalDB** es una instancia de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] que puede crear y abrir las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Los archivos de base de datos del sistema para la base de datos se almacenan normalmente en la ruta de acceso de AppData local de los usuarios, que suele estar oculta. Por ejemplo, **C:\Users\\<usuario\>\AppData\Local\Microsoft\Microsoft SQL Server Local DB\Instances\LocalDBApp1\\**. Los archivos de base de datos de usuario se almacenan donde indique el usuario, normalmente en alguna ubicación de la carpeta **C:\Usuarios\\<usuario\>\Documentos\\**.  
  
 Para obtener más información sobre cómo incluir **LocalDB** en una aplicación, vea la documentación de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] [Información general de datos locales](http://msdn.microsoft.com/library/ms233817\(VS.110\).aspx), [Walkthrough: Creating a SQL Server LocalDB Database (Tutorial: creación de una base de datos LocalDB de SQL Server)](http://msdn.microsoft.com/library/ms233763\(VS.110\).aspx) y [Walkthrough: Connecting to Data in a SQL Server LocalDB Database (Windows Forms) (Tutorial: conexión a datos en una base de datos LocalDB de SQL Server (Windows Forms))](http://msdn.microsoft.com/library/ms171890\(VS.110\).aspx).  
  
 Para obtener más información acerca de la API **LocalDB** , vea [Referencia de la API de instancia de SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh234692\(SQL.110\).aspx) y [Función LocalDBStartInstance](http://msdn.microsoft.com/library/hh217143\(SQL.110\).aspx).  
  
 La utilidad SqlLocalDb puede crear nuevas instancias de **LocalDB**e iniciar y detener una instancia de **LocalDB**; incluye opciones para ayudarle a administrar **LocalDB**.  Para obtener más información sobre la utilidad SqlLocalDb, vea [SqlLocalDB (utilidad)](../../tools/sqllocaldb-utility.md).  
  
 La intercalación de la instancia de **LocalDB** está establecida en SQL_Latin1_General_CP1_CI_AS y no se puede cambiar. Normalmente se admiten las intercalaciones de nivel de base de datos, nivel de columna y nivel de expresión. Las bases de datos independientes siguen las reglas de las intercalaciones de metadatos y tempdb definidas por [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md).  
  
### <a name="restrictions"></a>Restricciones  
 **LocalDB** no puede ser un suscriptor de replicación de mezcla.  
  
 **LocalDB** no admite FILESTREAM.  
  
 **LocalDB** solo permite colas locales de Service Broker.  
  
 Una instancia de **LocalDB** propiedad de cuentas integradas, como NT AUTHORITY\SYSTEM, puede presentar problemas de administrabilidad debido a la redirección del sistema de archivos de Windows. En su lugar, puede usar una cuenta de Windows normal como propietario.  
  
### <a name="automatic-and-named-instances"></a>Instancias automáticas y con nombre  
 **LocalDB** admite dos tipos de instancias: instancias automáticas e instancias con nombre.  
  
-   Las instancias automáticas de **LocalDB** son públicas. Se crean y se administran automáticamente para el usuario y se pueden utilizar en cualquier aplicación. Hay una instancia automática de **LocalDB** en cada versión de **LocalDB** instalada en el equipo del usuario. Las instancias automáticas de **LocalDB** proporcionan una administración agilizada de la instancia. No hay ninguna necesidad de crear la instancia; solo funciona. Esto permite la instalación y migración fáciles de las aplicaciones en un equipo diferente. Si la máquina de destino tiene la versión especificada de **LocalDB** instalada, la instancia automática de **LocalDB** de esa versión también estará disponible en la máquina de destino. Las instancias automáticas de **LocalDB** cuentan con un patrón especial para el nombre de instancia que pertenece a un espacio de nombres reservado. Esto evita conflictos de nombres con las instancias con nombre de **LocalDB**. El nombre de la instancia automática es **MSSQLLocalDB**.  
  
-   Las instancias con nombre de **LocalDB** son privadas. Son propiedad de una sola aplicación que es la responsable de la creación y administración de la instancia. Las instancias con nombre proporcionan el aislamiento de otras instancias y pueden mejorar el rendimiento reduciendo la contención de recursos con otros usuarios de bases de datos. Las instancias con nombre deben ser creadas explícitamente por el usuario a través de la API de administración de **LocalDB** o implícitamente a través del archivo app.config de una aplicación administrada (aunque la aplicación administrada también puede usar la API, si así lo quiere). Cada instancia con nombre de **LocalDB** tiene una versión de **LocalDB** asociada que señala al conjunto respectivo de binarios de **LocalDB** . El nombre de instancia de **LocalDB** es de tipo de datos **sysname** y puede tener hasta 128 caracteres. (Esta característica es diferente para las instancias con nombre normales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], en que los nombres están limitados a nombres de NetBIOS normales de 16 caracteres ASCII). El nombre de una instancia de **LocalDB** puede contener cualquier tipo de caracteres Unicode que sean válidos en un nombre de archivo.  Una instancia con nombre que utiliza un nombre de instancia automática se convierte en una instancia automática.  
  
 Usuarios diferentes de un equipo pueden tener instancias con el mismo nombre. Cada instancia es un proceso diferente que se ejecuta como un usuario diferente.  
  
## <a name="shared-instances-of-localdb"></a>Instancias compartidas de LocalDB  
 Para admitir escenarios donde varios usuarios del equipo deben conectarse a una instancia de **LocalDB**, **LocalDB** admite el uso compartido de la instancia. Un propietario de una instancia puede decidir permitir que otros usuarios del equipo se conecten a la instancia. Las instancias tanto automáticas como con nombre de **LocalDB** se pueden compartir. Para compartir una instancia de **LocalDB** , un usuario selecciona un nombre compartido (alias) para ella. Dado que el nombre compartido está visible para todos los usuarios del equipo, este nombre compartido debe ser único en el equipo. El nombre compartido para una instancia de **LocalDB** tiene el mismo formato que la instancia con nombre de **LocalDB**.  
  
 Solo un administrador del equipo puede crear una instancia compartida de **LocalDB**. Una instancia compartida de **LocalDB** puede dejar de ser compartida por la acción de un administrador o el propietario de la instancia compartida de **LocalDB**. Para compartir y dejar de compartir una instancia de **LocalDB**, use los métodos `LocalDBShareInstance` y `LocalDBUnShareInstance` de la API de **LocalDB** o las opciones para compartir y no compartir de la utilidad SqlLocalDb.  
  
## <a name="starting-localdb-and-connecting-to-localdb"></a>Iniciar LocalDB y conectarse a LocalDB  
  
### <a name="connecting-to-the-automatic-instance"></a>Conectarse con la instancia automática  
 La manera más fácil de usar **LocalDB** es conectarse a la instancia automática propiedad del usuario actual mediante la cadena de conexión **"Server=(localdb)\MSSQLLocalDB;Integrated Security=true"**. Para conectarse a una base de datos concreta con el nombre de archivo, conéctese mediante una cadena de conexión similar a **"Server=(LocalDB)\MSSQLLocalDB; Integrated Security=true ;AttachDbFileName=D:\Data\MyDB1.mdf"**.  
  
> [!NOTE]  
>  La primera vez que un usuario de un equipo intenta conectarse a **LocalDB**, se debe crear e iniciar la instancia automática. El tiempo adicional para la creación de la instancia puede hacer que el intento de conexión deje de funcionar con un mensaje de fin de tiempo de espera. Cuando sucede esto, espere unos segundos para que el proceso de creación se complete y, a continuación, conéctese de nuevo.  
  
### <a name="creating-and-connecting-to-a-named-instances"></a>Crear instancias con nombre y conectarse a ellas  
 Además de la instancia automática, **LocalDB** también admite instancias con nombre. Use el programa SqlLocalDB.exe para crear, iniciar y detener una instancia con nombre de **LocalDB**. Para obtener más información sobre SqlLocalDB.exe, vea [SqlLocalDB (utilidad)](../../tools/sqllocaldb-utility.md).  
  
```ms-dos  
REM Create an instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\130\Tools\Binn\SqlLocalDB.exe" create LocalDBApp1  
REM Start the instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\130\Tools\Binn\SqlLocalDB.exe" start LocalDBApp1  
REM Gather information about the instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\130\Tools\Binn\SqlLocalDB.exe" info LocalDBApp1  
```  
  
 La última línea anterior devuelve información similar a la siguiente.  
  
|||  
|-|-|  
|Nombre|"LocalDBApp1"|  
|Versión|\<Versión actual>|  
|Nombre compartido|""|  
|Propietario|"\<Su usuario de Windows>"|  
|Creación automática|No|  
|State|ejecución|  
|Última hora de inicio|\<Fecha y hora>|  
|Nombre de canalización de instancia|np:\\\\.\pipe\LOCALDB#F365A78E\tsql\query|  
  
> [!NOTE]  
>  Si la aplicación utiliza una versión de .NET anterior a 4.0.2, debe conectarse directamente a la canalización con nombre de **LocalDB**. El valor Nombre de canalización de instancia es la canalización con nombre en la que escucha la instancia de **LocalDB** . La parte de Nombre de canalización de instancia que sigue a LOCALDB# cambiará cada vez que se inicie la instancia de **LocalDB**. Para conectarse a la instancia de **LocalDB** mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], escriba el nombre de canalización de instancia en el cuadro **Nombre de servidor** del cuadro de diálogo **Conectar al [!INCLUDE[ssDE](../../includes/ssde-md.md)]**. Desde su programa personalizado puede establecer la conexión a la instancia de **LocalDB** mediante una cadena de conexión similar a `SqlConnection conn = new SqlConnection(@"Server=np:\\.\pipe\LOCALDB#F365A78E\tsql\query");`  
  
### <a name="connecting-to-a-shared-instance-of-localdb"></a>Conectarse a una instancia compartida de LocalDB  
 Para conectarse a una instancia compartida de **LocalDB** , agregue **.\\** (punto + barra diagonal inversa) a la cadena de conexión para hacer referencia al espacio de nombres reservado para las instancias compartidas. Por ejemplo, para conectarse a una instancia compartida de **LocalDB** denominada `AppData` , use una cadena de conexión, como `(localdb)\.\AppData` , como parte de la cadena de conexión. Un usuario que se conecta a una instancia compartida de **LocalDB** de la que no es propietario debe tener un inicio de sesión con autenticación de Windows o autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="troubleshooting"></a>Solucionar problemas  
 Para obtener información sobre cómo solucionar problemas de **LocalDB**, vea la página que trata la [solución de problemas de SQL Server 2012 Express LocalDB](http://social.technet.microsoft.com/wiki/contents/articles/4609.aspx).  
  
## <a name="permissions"></a>Permisos  
 Una instancia de [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)]**LocalDB** es una instancia creada por el usuario para utilizarla. Cualquier usuario del equipo puede crear una base de datos usando una instancia de **LocalDB**, almacenando archivos en su perfil de usuario y ejecutando el proceso con sus credenciales. De forma predeterminada, el acceso a la instancia de **LocalDB** está limitado a su propietario. Los datos contenidos en **LocalDB** están protegidos por el acceso al sistema de archivos en los archivos de base de datos. Si los archivos de base de datos de usuario se almacenan en una ubicación compartida, cualquiera que tenga acceso al sistema de archivos en esa ubicación puede abrir la base de datos usando una instancia de **LocalDB** que sea de su propiedad. Si los archivos de base de datos están en una ubicación protegida, como la carpeta de datos de los usuarios, solo el usuario y los administradores con acceso a la carpeta pueden abrir la base de datos. Los archivos de **LocalDB** solo los puede abrir una instancia de **LocalDB** cada vez.  
  
> [!NOTE]  
>  **LocalDB** siempre se ejecuta en el contexto de seguridad de los usuarios; es decir, **LocalDB** nunca se ejecuta con credenciales del grupo local Administradores. Esto significa que todos los archivos de base de datos usados por una instancia de **LocalDB** deben ser accesibles mediante la cuenta de Windows del usuario propietario, sin considerar la pertenencia al grupo local Administradores.  
  
## <a name="see-also"></a>Vea también  
 [SqlLocalDB (utilidad)](../../tools/sqllocaldb-utility.md)  
  
  

