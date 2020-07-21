---
title: SQL Server 2014 Express LocalDB | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- user instances
- LocalDB, described
- local database runtime
- file database
- LocalDB
ms.assetid: 5a641a46-7cfb-4d7b-a90d-6e4625719d74
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f3c43604604580c5924be4daf4d473407564d247
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934886"
---
# <a name="sql-server-2014-express-localdb"></a>SQL Server 2014 Express LocalDB
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] `LocalDB` es un modo de ejecución de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] destinado a los desarrolladores de programas. `LocalDB`la instalación copia un conjunto mínimo de archivos necesarios para iniciar el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . Una vez `LocalDB` instalado, los desarrolladores inician una conexión mediante una cadena de conexión especial. Cuando se realiza la conexión, se crea y se inicia automáticamente la infraestructura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] necesaria, permitiendo que la aplicación use la base de datos sin tareas de configuración complejas o prolongadas en el tiempo. Las herramientas de desarrollo pueden proporcionar a los desarrolladores de software un [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que les permite escribir y probar el código de [!INCLUDE[tsql](../../includes/tsql-md.md)] sin tener que administrar una instancia de servidor completa de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Una instancia de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] `LocalDB` se administra mediante la `SqlLocalDB.exe` utilidad. [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]`LocalDB`debe usarse en lugar de la [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] característica de instancia de usuario, que está en desuso.  
  
## <a name="installing-localdb"></a>Instalar LocalDB  
 El método principal de instalación `LocalDB` es mediante el programa SqlLocalDB.msi. `LocalDB`es una opción al instalar cualquier SKU de [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] . Seleccione `LocalDB` en la página **selección de características** durante la instalación de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] . Solo puede haber una instalación de los `LocalDB` archivos binarios para cada [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] versión principal. Se pueden iniciar varios procesos de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y todos usarán los mismos binarios. Una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] iniciado como `LocalDB` tiene las mismas limitaciones que[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]  
  
## <a name="description"></a>Descripción  
 El `LocalDB` programa de instalación utiliza el programa SqlLocalDB.msi para instalar los archivos necesarios en el equipo. Una vez instalada, `LocalDB` es una instancia de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] que puede crear y abrir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bases de datos de. Los archivos de base de datos del sistema para la base de datos se almacenan normalmente en la ruta de acceso de AppData local de los usuarios, que suele estar oculta. Por ejemplo, **C:\Users\\<usuario\>\AppData\Local\Microsoft\Microsoft SQL Server Local DB\Instances\LocalDBApp1\\**. Los archivos de base de datos de usuario se almacenan donde indique el usuario, normalmente en alguna ubicación de la carpeta **C:\Usuarios\\<usuario\>\Documentos\\**.  
  
 Para obtener más información acerca `LocalDB` de cómo incluir en una aplicación, consulte la [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] documentación [información general sobre datos locales](https://msdn.microsoft.com/library/ms233817\(VS.110\).aspx), [Tutorial: creación de una base](https://msdn.microsoft.com/library/ms233763\(VS.110\).aspx)de datos de SQL Server LocalDB y [tutorial: conectarse a datos en una SQL Server base de datos LocalDB (Windows Forms)](https://msdn.microsoft.com/library/ms171890\(VS.110\).aspx).  
  
 Para obtener más información sobre la `LocalDB` API, vea [SQL Server Express referencia de API de instancia de LocalDB](https://msdn.microsoft.com/library/hh234692\(SQL.110\).aspx) y la [función LocalDBStartInstance](https://msdn.microsoft.com/library/hh217143\(SQL.110\).aspx).  
  
 La utilidad SqlLocalDb puede crear nuevas instancias de `LocalDB` , iniciar y detener una instancia de `LocalDB` , e incluye opciones para ayudarle a administrar `LocalDB` .  Para obtener más información sobre la utilidad SqlLocalDb, vea [SqlLocalDB (utilidad)](../../tools/sqllocaldb-utility.md).  
  
 La intercalación de la instancia de `LocalDB` está establecida en SQL_LATIN1_GENERAL_CP1_CI_AS y no se puede cambiar. Normalmente se admiten las intercalaciones de nivel de base de datos, nivel de columna y nivel de expresión. Las bases de datos independientes siguen las reglas de las intercalaciones de metadatos y tempdb definidas por [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md).  
  
### <a name="restrictions"></a>Restricciones  
 `LocalDB`no puede ser un suscriptor de replicación de mezcla.  
  
 `LocalDB`no admite FILESTREAM.  
  
 `LocalDB`solo permite colas locales para Service Broker.  
  
 Una instancia de `LocalDB` propiedad de las cuentas integradas, como NT AUTHORITY\SYSTEM, puede tener problemas de capacidad de administración debido a la redirección del sistema de archivos de Windows. En su lugar, use una cuenta de Windows normal como propietario.  
  
### <a name="automatic-and-named-instances"></a>Instancias automáticas y con nombre  
 `LocalDB`admite dos tipos de instancias: instancias automáticas e instancias con nombre.  
  
-   Las instancias automáticas de `LocalDB` son públicas. Se crean y se administran automáticamente para el usuario y se pueden utilizar en cualquier aplicación. Existe una instancia automática de `LocalDB` para cada versión de `LocalDB` instalada en el equipo del usuario. Las instancias automáticas de `LocalDB` proporcionan administración de instancias sin problemas. No hay ninguna necesidad de crear la instancia; solo funciona. Esto permite la instalación y migración fáciles de las aplicaciones en un equipo diferente. Si la máquina de destino tiene la versión especificada de `LocalDB` instalada, la instancia automática de `LocalDB` de esa versión también estará disponible en la máquina de destino. Las instancias automáticas de `LocalDB` tienen un patrón especial para el nombre de instancia que pertenece a un espacio de nombres reservado. Esto evita conflictos de nombres con las instancias con nombre de `LocalDB` . El nombre de la instancia automática es **MSSQLLocalDB**.  
  
-   Las instancias con nombre de `LocalDB` son privadas. Son propiedad de una sola aplicación que es la responsable de la creación y administración de la instancia. Las instancias con nombre proporcionan el aislamiento de otras instancias y pueden mejorar el rendimiento reduciendo la contención de recursos con otros usuarios de bases de datos. El usuario debe crear explícitamente las instancias con nombre a través de la `LocalDB` API de administración o implícitamente a través del archivo de app.config para una aplicación administrada (aunque la aplicación administrada también puede usar la API, si lo desea). Cada instancia con nombre de `LocalDB` tiene una `LocalDB` versión asociada que señala al conjunto respectivo de `LocalDB` binarios. El nombre de instancia de un `LocalDB` tipo de datos de es `sysname` y puede tener hasta 128 caracteres. (Esto difiere de las instancias con nombre normales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , que limita los nombres a nombres NetBIOS normales de 16 caracteres ASCII). El nombre de una instancia de `LocalDB` puede contener cualquier carácter Unicode que sea válido dentro de un nombre de archivo.  Una instancia con nombre que utiliza un nombre de instancia automática se convierte en una instancia automática.  
  
 Usuarios diferentes de un equipo pueden tener instancias con el mismo nombre. Cada instancia es un proceso diferente que se ejecuta como un usuario diferente.  
  
## <a name="shared-instances-of-localdb"></a>Instancias compartidas de LocalDB  
 Para admitir escenarios donde varios usuarios del equipo necesitan conectarse a una sola instancia de `LocalDB` , admite el `LocalDB` uso compartido de instancias. Un propietario de una instancia puede decidir permitir que otros usuarios del equipo se conecten a la instancia. Se pueden compartir instancias automáticas y con nombre de `LocalDB` . Para compartir una instancia de `LocalDB`, un usuario selecciona un nombre compartido (alias) para ella. Dado que el nombre compartido está visible para todos los usuarios del equipo, este nombre compartido debe ser único en el equipo. El nombre compartido de una instancia de `LocalDB` tiene el mismo formato que la instancia con nombre de `LocalDB` .  
  
 Solo un administrador del equipo puede crear una instancia compartida de `LocalDB` . Un `LocalDB` Administrador o el propietario de la instancia compartida de pueden dejar de compartir una instancia compartida de `LocalDB` . Para compartir y dejar de compartir una instancia de `LocalDB` , use los `LocalDBShareInstance` `LocalDBUnShareInstance` métodos y de la `LocalDB` API, o las opciones compartir y no compartir de la utilidad SqlLocalDb.  
  
## <a name="starting-localdb-and-connecting-to-localdb"></a>Iniciar LocalDB y conectarse a LocalDB  
  
### <a name="connecting-to-the-automatic-instance"></a>Conectarse con la instancia automática  
 La forma más fácil de usar `LocalDB` es conectarse a la instancia automática propiedad del usuario actual mediante la cadena de conexión **"Server = (LocalDB) \MSSQLLocalDB; Integrated Security = true"**. Para conectarse a una base de datos concreta con el nombre de archivo, conéctese mediante una cadena de conexión similar a **"Server=(LocalDB)\MSSQLLocalDB; Integrated Security=true ;AttachDbFileName=D:\Data\MyDB1.mdf"**.  
  
> [!NOTE]  
>  La primera vez que un usuario de un equipo intenta conectarse a `LocalDB` , se debe crear e iniciar la instancia automática. El tiempo adicional para la creación de la instancia puede hacer que el intento de conexión deje de funcionar con un mensaje de fin de tiempo de espera. Cuando sucede esto, espere unos segundos para que el proceso de creación se complete y, a continuación, conéctese de nuevo.  
  
### <a name="creating-and-connecting-to-a-named-instances"></a>Crear instancias con nombre y conectarse a ellas  
 Además de la instancia automática, `LocalDB` también admite instancias con nombre. Utilice el programa SqlLocalDB.exe para crear, iniciar y detener una instancia con nombre de `LocalDB` . Para obtener más información sobre SqlLocalDB.exe, vea [SqlLocalDB (utilidad)](../../tools/sqllocaldb-utility.md).  
  
```ms-dos  
REM Create an instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\120\Tools\Binn\SqlLocalDB.exe" create LocalDBApp1  
REM Start the instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\120\Tools\Binn\SqlLocalDB.exe" start LocalDBApp1  
REM Gather information about the instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\120\Tools\Binn\SqlLocalDB.exe" info LocalDBApp1  
```  
  
 La última línea anterior devuelve información similar a la siguiente.  
  
|||  
|-|-|  
|Nombre|"LocalDBApp1"|  
|Versión|\<Current Version>|  
|Nombre compartido|""|  
|Propietario|"\<Your Windows User>"|  
|Creación automática|No|  
|State|en ejecución|  
|Última hora de inicio|\<Date and Time>|  
|Nombre de canalización de instancia|np:\\\\.\pipe\LOCALDB#F365A78E\tsql\query|  
  
> [!NOTE]  
>  Si su aplicación usa una versión de .NET anterior a la 4.0.2, debe conectarse directamente a la canalización con nombre de `LocalDB` . El valor de nombre de canalización de instancia es la canalización con nombre en la que escucha la instancia de `LocalDB` . La parte del nombre de la canalización de la instancia después de LOCALDB # cambiará cada vez que se inicie la instancia de `LocalDB` . Para conectarse a la instancia de mediante `LocalDB` [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , escriba el nombre de la canalización de instancia en el cuadro **nombre del servidor** del cuadro de diálogo **conectar con [!INCLUDE[ssDE](../../includes/ssde-md.md)] ** . En el programa personalizado puede establecer conexión con la instancia de `LocalDB` mediante una cadena de conexión similar a`SqlConnection conn = new SqlConnection(@"Server=np:\\.\pipe\LOCALDB#F365A78E\tsql\query");`  
  
### <a name="connecting-to-a-shared-instance-of-localdb"></a>Conectarse a una instancia compartida de LocalDB  
 Para conectarse a una instancia compartida de `LocalDB` Add ** \\ ** (punto + barra diagonal inversa) a la cadena de conexión para hacer referencia al espacio de nombres reservado para las instancias compartidas. Por ejemplo, para conectarse a una instancia compartida de `LocalDB` denominada, `AppData` use una cadena de conexión como `(localdb)\.\AppData` como parte de la cadena de conexión. Un usuario que se conecta a una instancia compartida de `LocalDB` que no es de su propiedad debe tener un inicio de sesión de autenticación de Windows o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación de.  
  
## <a name="troubleshooting"></a>Solucionar problemas  
 Para obtener información acerca de la solución de problemas `LocalDB` , consulte [solución de problemas SQL Server 2012 Express LocalDB](https://social.technet.microsoft.com/wiki/contents/articles/4609.aspx).  
  
## <a name="permissions"></a>Permisos  
 Una instancia de [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] `LocalDB` es una instancia creada por un usuario para su uso. Cualquier usuario del equipo puede crear una base de datos mediante una instancia de `LocalDB` , almacenando archivos en su perfil de usuario y ejecutando el proceso con sus credenciales. De forma predeterminada, el acceso a la instancia de `LocalDB` está limitado a su propietario. Los datos contenidos en `LocalDB` están protegidos por el acceso al sistema de archivos a los archivos de base de datos. Si los archivos de base de datos de usuario se almacenan en una ubicación compartida, cualquier usuario con acceso al sistema de archivos en esa ubicación puede abrir la base de datos mediante una instancia de la `LocalDB` que poseen. Si los archivos de base de datos están en una ubicación protegida, como la carpeta de datos de los usuarios, solo el usuario y los administradores con acceso a la carpeta pueden abrir la base de datos. Los `LocalDB` archivos solo se pueden abrir en una instancia de `LocalDB` a la vez.  
  
> [!NOTE]  
>  `LocalDB`siempre se ejecuta en el contexto de seguridad de los usuarios. es decir, `LocalDB` nunca se ejecuta con credenciales del grupo de administradores locales. Esto significa que todos los archivos de base de datos usados por una `LocalDB` instancia de deben ser accesibles mediante la cuenta de Windows del usuario propietario, sin considerar la pertenencia al grupo local Administradores.  
  
## <a name="see-also"></a>Consulte también  
 [SqlLocalDB (utilidad)](../../tools/sqllocaldb-utility.md)  
  
  
