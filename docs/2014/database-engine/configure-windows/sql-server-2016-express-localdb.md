---
title: SQL Server 2014 Express LocalDB | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- user instances
- LocalDB, described
- local database runtime
- file database
- LocalDB
ms.assetid: 5a641a46-7cfb-4d7b-a90d-6e4625719d74
caps.latest.revision: 30
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d87a85927751b12e3f86d5ce2bc908da9d063b21
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37243255"
---
# <a name="sql-server-2014-express-localdb"></a>SQL Server 2014 Express LocalDB
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] `LocalDB` es un modo de ejecución de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] destinado a los desarrolladores de programa. `LocalDB` instalación copia un conjunto mínimo de archivos necesarios para iniciar el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Una vez `LocalDB` está instalado, los desarrolladores inician una conexión mediante el uso de una cadena de conexión especial. Cuando se conecta el necesario [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] infraestructura es automáticamente crea e inicia, permitiendo que la aplicación usar la base de datos sin tareas de configuración compleja ni tardar mucho tiempo. Las herramientas de desarrollo pueden proporcionar a los desarrolladores de software un [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que les permite escribir y probar el código de [!INCLUDE[tsql](../../includes/tsql-md.md)] sin tener que administrar una instancia de servidor completa de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Una instancia de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] `LocalDB` se administra mediante el `SqlLocalDB.exe` utilidad. [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]`LocalDB` debe usarse en lugar de la [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] característica de instancia de usuario que está en desuso.  
  
## <a name="installing-localdb"></a>Instalar LocalDB  
 El principal método de instalación `LocalDB` es mediante el programa SqlLocalDB.msi. `LocalDB` es una opción al instalar cualquier SKU de [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)]. Seleccione `LocalDB` en el **selección de características** página durante la instalación de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. Puede haber solo una instalación de la `LocalDB` archivos binarios para cada versión principal [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] versión. Se pueden iniciar varios procesos de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y todos usarán los mismos binarios. Una instancia de la [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] comenzó como el `LocalDB` tiene las mismas limitaciones que [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]  
  
## <a name="description"></a>Descripción  
 El `LocalDB` programa de instalación utiliza el programa SqlLocalDB.msi para instalar los archivos necesarios en el equipo. Una vez instalado, `LocalDB` es una instancia de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] que puede crear y abrir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bases de datos. Los archivos de base de datos del sistema para la base de datos se almacenan normalmente en la ruta de acceso de AppData local de los usuarios, que suele estar oculta. Por ejemplo, **C:\Users\\<usuario\>\AppData\Local\Microsoft\Microsoft SQL Server Local DB\Instances\LocalDBApp1\\**. Los archivos de base de datos de usuario se almacenan donde indique el usuario, normalmente en alguna ubicación de la carpeta **C:\Usuarios\\<usuario\>\Documentos\\**.  
  
 Para obtener más información acerca de cómo incluir `LocalDB` en una aplicación, consulte el [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] documentación [Local Data Overview](http://msdn.microsoft.com/library/ms233817\(VS.110\).aspx), [Tutorial: crear una base de datos de SQL Server LocalDB](http://msdn.microsoft.com/library/ms233763\(VS.110\).aspx), y [Tutorial: conectarse a datos en una base de datos SQL Server LocalDB (Windows Forms)](http://msdn.microsoft.com/library/ms171890\(VS.110\).aspx).  
  
 Para obtener más información sobre la `LocalDB` API, consulte [referencia de SQL Server Express LocalDB instancia API](http://msdn.microsoft.com/library/hh234692\(SQL.110\).aspx) y [función LocalDBStartInstance](http://msdn.microsoft.com/library/hh217143\(SQL.110\).aspx).  
  
 La utilidad SqlLocalDb puede crear nuevas instancias de `LocalDB`, iniciar y detener una instancia de `LocalDB`e incluye opciones para ayudarle a administrar `LocalDB`.  Para obtener más información sobre la utilidad SqlLocalDb, vea [SqlLocalDB (utilidad)](../../tools/sqllocaldb-utility.md).  
  
 La intercalación de la instancia para `LocalDB` está establecida en SQL_Latin1_General_CP1_CI_AS y no se puede cambiar. Normalmente se admiten las intercalaciones de nivel de base de datos, nivel de columna y nivel de expresión. Las bases de datos independientes siguen las reglas de las intercalaciones de metadatos y tempdb definidas por [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md).  
  
### <a name="restrictions"></a>Restrictions  
 `LocalDB` no puede ser un suscriptor de replicación de mezcla.  
  
 `LocalDB` no se admite FILESTREAM.  
  
 `LocalDB` solo permite colas locales de Service Broker.  
  
 Una instancia de `LocalDB` pertenecen a las cuentas integradas como NT AUTHORITY\SYSTEM puede presentar problemas de administrabilidad debido a la redirección del sistema de archivos de windows. En su lugar, use una cuenta de windows normal como propietario.  
  
### <a name="automatic-and-named-instances"></a>Instancias automáticas y con nombre  
 `LocalDB` admite dos tipos de instancias: instancias automáticas e instancias con nombre.  
  
-   Las instancias automáticas de `LocalDB` son públicos. Se crean y se administran automáticamente para el usuario y se pueden utilizar en cualquier aplicación. Una instancia automática de `LocalDB` en cada versión de `LocalDB` instalado en el equipo del usuario. Las instancias automáticas de `LocalDB` proporcionar una administración agilizada de la instancia. No hay ninguna necesidad de crear la instancia; solo funciona. Esto permite la instalación y migración fáciles de las aplicaciones en un equipo diferente. Si el equipo de destino tiene la versión especificada de `LocalDB` instalada, la instancia automática de `LocalDB` para esa versión está disponible en el equipo de destino. Las instancias automáticas de `LocalDB` cuentan con un patrón especial para el nombre de instancia que pertenece a un espacio de nombres reservado. Esto evita conflictos de nombres con las instancias con nombre de `LocalDB`. El nombre de la instancia automática es **MSSQLLocalDB**.  
  
-   Instancias con nombre de `LocalDB` son privados. Son propiedad de una sola aplicación que es la responsable de la creación y administración de la instancia. Las instancias con nombre proporcionan el aislamiento de otras instancias y pueden mejorar el rendimiento reduciendo la contención de recursos con otros usuarios de bases de datos. Las instancias con nombre deben ser creadas explícitamente por el usuario a través de la `LocalDB` API de administración o implícitamente a través del archivo app.config de archivos para una aplicación administrada (aunque la aplicación administrada también puede usar la API, si lo desea). Cada instancia con nombre de `LocalDB` tiene asociado un `LocalDB` versión que señala al conjunto respectivo de `LocalDB` archivos binarios. El nombre de instancia de un `LocalDB` es `sysname` datos escriba y puede tener hasta 128 caracteres. (Esta característica es diferente para las instancias con nombre normales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], en que los nombres están limitados a nombres de NetBIOS normales de 16 caracteres ASCII). Esto significa que todos los archivos base de datos utilizados por un `LocalDB` instancia debe ser accesible mediante la cuenta de Windows del usuario propietario, sin considerar la pertenencia al grupo Administradores local.  Una instancia con nombre que utiliza un nombre de instancia automática se convierte en una instancia automática.  
  
 Usuarios diferentes de un equipo pueden tener instancias con el mismo nombre. Cada instancia es un proceso diferente que se ejecuta como un usuario diferente.  
  
## <a name="shared-instances-of-localdb"></a>Instancias compartidas de LocalDB  
 Para admitir escenarios donde varios usuarios del equipo deben conectarse a una sola instancia de `LocalDB`, `LocalDB` admite el uso compartido de la instancia. Un propietario de una instancia puede decidir permitir que otros usuarios del equipo se conecten a la instancia. Las instancias tanto automáticas como con nombre de `LocalDB` pueden compartirse. Para compartir una instancia de `LocalDB` un usuario selecciona un nombre compartido (alias) para ella. Dado que el nombre compartido está visible para todos los usuarios del equipo, este nombre compartido debe ser único en el equipo. El nombre compartido para una instancia de `LocalDB` tiene el mismo formato que la instancia mencionada de `LocalDB`.  
  
 Solo un administrador en el equipo puede crear una instancia compartida de `LocalDB`. Una instancia compartida de `LocalDB` puede compartirse por un administrador o el propietario de la instancia compartida de `LocalDB`. Para compartir y dejar una instancia de `LocalDB`, utilice el `LocalDBShareInstance` y `LocalDBUnShareInstance` métodos de la `LocalDB` API, o el recurso compartido y opciones de la utilidad SqlLocalDb.  
  
## <a name="starting-localdb-and-connecting-to-localdb"></a>Iniciar LocalDB y conectarse a LocalDB  
  
### <a name="connecting-to-the-automatic-instance"></a>Conectarse con la instancia automática  
 La manera más fácil de usar `LocalDB` consiste en conectar a la instancia automática propiedad del usuario actual mediante el uso de la cadena de conexión **"Server = (localdb) \MSSQLLocalDB;Integrated Security = true"**. Para conectarse a una base de datos concreta con el nombre de archivo, conéctese mediante una cadena de conexión similar a **"Server=(LocalDB)\MSSQLLocalDB; Integrated Security=true ;AttachDbFileName=D:\Data\MyDB1.mdf"**.  
  
> [!NOTE]  
>  La primera vez que un usuario en un equipo intenta conectarse a `LocalDB`, la instancia automática debe ser tanto se crea y se inicia. El tiempo adicional para la creación de la instancia puede hacer que el intento de conexión deje de funcionar con un mensaje de fin de tiempo de espera. Cuando sucede esto, espere unos segundos para que el proceso de creación se complete y, a continuación, conéctese de nuevo.  
  
### <a name="creating-and-connecting-to-a-named-instances"></a>Crear instancias con nombre y conectarse a ellas  
 Además de la instancia automática, `LocalDB` también admite instancias con nombre. Use el programa SqlLocalDB.exe para crear, iniciar y detener una instancia con nombre de `LocalDB`. Para obtener más información sobre SqlLocalDB.exe, vea [SqlLocalDB (utilidad)](../../tools/sqllocaldb-utility.md).  
  
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
|Versión|\<Versión actual>|  
|Nombre compartido|""|  
|Propietario|"\<Su usuario de Windows>"|  
|Creación automática|no|  
|State|ejecución|  
|Última hora de inicio|\<Fecha y hora>|  
|Nombre de canalización de instancia|np:\\\\.\pipe\LOCALDB#F365A78E\tsql\query|  
  
> [!NOTE]  
>  Si la aplicación usa una versión de .NET anterior a 4.0.2 debe conectarse directamente a la canalización con nombre de la `LocalDB`. El valor de nombre de canalización de instancia es la canalización con nombre que la instancia de `LocalDB` está escuchando. La parte del nombre de la canalización de instancia después de que LOCALDB # cambiará cada vez la instancia de `LocalDB` se inicia. Para conectarse a la instancia de `LocalDB` utilizando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], escriba el nombre de la canalización de instancia en el **nombre del servidor** cuadro de la **conectarse a [!INCLUDE[ssDE](../../includes/ssde-md.md)]**  cuadro de diálogo. En su programa personalizado puede establecer la conexión a la instancia de `LocalDB` mediante una cadena de conexión similar a `SqlConnection conn = new SqlConnection(@"Server=np:\\.\pipe\LOCALDB#F365A78E\tsql\query");`  
  
### <a name="connecting-to-a-shared-instance-of-localdb"></a>Conectarse a una instancia compartida de LocalDB  
 Para conectarse a una instancia compartida de `LocalDB` agregar **.\\**  (punto + barra diagonal inversa) a la cadena de conexión para hacer referencia el espacio de nombres reservado para las instancias compartidas. Por ejemplo, para conectarse a una instancia compartida de `LocalDB` denominado `AppData` usar, como una cadena de conexión `(localdb)\.\AppData` como parte de la cadena de conexión. Un usuario se conecta a una instancia compartida de `LocalDB` que no es propietario debe tener una autenticación de Windows o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión de autenticación.  
  
## <a name="troubleshooting"></a>Solucionar problemas  
 Para obtener información acerca de cómo solucionar `LocalDB`, consulte [solución de problemas de SQL Server 2012 Express LocalDB](http://social.technet.microsoft.com/wiki/contents/articles/4609.aspx).  
  
## <a name="permissions"></a>Permisos  
 Una instancia de [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] `LocalDB` es una instancia creada por el usuario para su uso. Cualquier usuario en el equipo puede crear una base de datos mediante una instancia de `LocalDB`, almacenando archivos en su perfil de usuario y ejecutando el proceso con sus credenciales. De forma predeterminada, el acceso a la instancia de `LocalDB` está limitado a su propietario. Los datos contenidos en el `LocalDB` está protegido por el sistema de archivos acceso a los archivos de base de datos. Si los archivos de base de datos de usuario se almacenan en una ubicación compartida, la base de datos se puede abrir cualquier persona con acceso al sistema de archivos en esa ubicación mediante el uso de una instancia de `LocalDB` que les pertenecen. Si los archivos de base de datos están en una ubicación protegida, como la carpeta de datos de los usuarios, solo el usuario y los administradores con acceso a la carpeta pueden abrir la base de datos. El `LocalDB` sólo se pueden abrir archivos mediante una instancia de `LocalDB` a la vez.  
  
> [!NOTE]  
>  `LocalDB` siempre se ejecuta en el contexto de seguridad de los usuarios; es decir, `LocalDB` nunca se ejecuta con las credenciales del grupo de administradores locales. Esto significa que todos los archivos base de datos utilizados por un `LocalDB` instancia debe ser accesible mediante la cuenta de Windows del usuario propietario, sin considerar la pertenencia al grupo Administradores local.  
  
## <a name="see-also"></a>Vea también  
 [SqlLocalDB (utilidad)](../../tools/sqllocaldb-utility.md)  
  
  
