---
title: Instancias de usuario de SQL Server Express
description: Describe la compatibilidad de las instancia de usuario de SQL Server Express.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 00c12376-cb26-4317-86ad-e6e9c089be57
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 91b00848fb42c64f1c180019a7618bf649488bd9
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896244"
---
# <a name="sql-server-express-user-instances"></a>Instancias de usuario de SQL Server Express

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Microsoft SQL Server Express Edition (SQL Server Express) admite la característica de la instancia de usuario, que solo está disponible cuando se usa el proveedor de datos SqlClient de Microsoft para SQL Server. Una instancia de usuario es una instancia independiente del motor de base de datos de SQL Server Express generada por una instancia primaria. Las instancias de usuario permiten a los usuarios que no son administradores de sus equipos locales adjuntar bases de datos de SQL Server Express y conectarse a ellas. Cada instancia se ejecuta en el contexto de seguridad del usuario individual, en un modelo de una instancia por usuario.  
  
## <a name="user-instance-capabilities"></a>Funcionalidades de la instancia de usuario  
Las instancias de usuario son útiles para los usuarios que ejecutan Windows con una cuenta de usuario con privilegios mínimos (LUA) porque cada usuario tiene privilegios de administrador del sistema SQL Server (`sysadmin`) a través de la instancia que se ejecuta en su equipo sin necesidad de ejecutarse también como administrador de Windows. El software que se ejecuta en una instancia de usuario con permisos limitados no puede realizar cambios en todo el sistema porque la instancia de SQL Server Express se está ejecutando bajo la cuenta de Windows del usuario que no es de administrador, no como servicio. Cada instancia de usuario está aislada de la instancia principal y de las demás instancias de usuario que se ejecutan en el mismo equipo. Las bases de datos que se ejecutan en una instancia de usuario se abren solo en modo de usuario único, y no es posible que varios usuarios se conecten a las bases de datos que se ejecutan en una instancia de usuario. La replicación y las consultas distribuidas también están deshabilitadas para las instancias de usuario.  
  
Para obtener más información, vea "Instancias de usuario" en los Libros en pantalla de SQL Server.  
  
> [!NOTE]
>  Las instancias de usuario no son necesarias para los usuarios que ya son administradores en sus propios equipos o para escenarios que implican a varios usuarios de base de datos.  
  
## <a name="enabling-user-instances"></a>Habilitación de instancias de usuario  
Para generar instancias de usuario, debe estar ejecutándose una instancia primaria de SQL Server Express. Las instancias de usuario se habilitan de forma predeterminada cuando se instala SQL Server Express y un administrador del sistema pueden habilitarlas o deshabilitarlas de forma explícita si ejecuta el procedimiento almacenado del sistema **sp_configure** en la instancia principal.  
  
```sql
-- Enable user instances.  
sp_configure 'user instances enabled','1'   
  
-- Disable user instances.  
sp_configure 'user instances enabled','0'  
```  
  
El protocolo de red para las instancias de usuario debe ser el de canalizaciones con nombre locales. No se puede iniciar una instancia de usuario en una instancia remota de SQL Server, y no se permiten inicios de sesión de SQL Server.  
  
## <a name="connecting-to-a-user-instance"></a>Conexión a una instancia de usuario  
Las palabras clave `User Instance` y `AttachDBFilename`<xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A> permiten a <xref:Microsoft.Data.SqlClient.SqlConnection> conectarse a una instancia de usuario. Las instancias de usuario también se admiten en las propiedades <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder>`UserInstance` y `AttachDBFilename`.  
  
Tenga en cuenta lo siguiente sobre la cadena de conexión de ejemplo que se muestra a continuación:  
  
- La palabra clave `Data Source` hace referencia a la instancia primaria de SQL Server Express que genera la instancia de usuario. La instancia predeterminada es .\sqlexpress.  
  
- `Integrated Security` se establece en `true`. Para conectarse a una instancia de usuario, se requiere la autenticación de Windows. No se admiten los inicios de sesión de SQL Server.  
  
- La propiedad `User Instance` se establece en `true`, lo cual invoca una instancia de usuario. (El valor predeterminado es `false`).  
  
- La palabra clave de cadena de conexión `AttachDbFileName` se utiliza para adjuntar el archivo de base de datos principal (.mdf), que debe incluir el nombre completo de la ruta de acceso. `AttachDbFileName` también se corresponde con las claves "propiedades extendidas" y "nombre de archivo inicial" dentro de una cadena de conexión de <xref:Microsoft.Data.SqlClient.SqlConnection>.  
  
- La cadena de sustitución de `|DataDirectory|` entre los símbolos de canalización hace referencia al directorio de datos de la aplicación que abre la conexión y proporciona una ruta de acceso relativa que indica la ubicación de los archivos de registro y la base de datos .mdf y.ldf. Si desea ubicar estos archivos en otro lugar, debe proporcionar la ruta de acceso completa a los archivos.  
  
```console
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;AttachDBFilename=|DataDirectory|\InstanceDB.mdf;  
Initial Catalog=InstanceDB;  
```  
  
> [!NOTE]
>  También puede usar las propiedades <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder><xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.UserInstance%2A> y <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.AttachDBFilename%2A> para crear una cadena de conexión en tiempo de ejecución.  
  
### <a name="using-the-124datadirectory124-substitution-string"></a>Uso de la cadena de sustitución &#124;DataDirectory&#124;  
`DataDirectory` se usa junto con `AttachDbFileName` para indicar una ruta de acceso relativa a un archivo de datos, lo que permite a los desarrolladores crear cadenas de conexión basadas en una ruta relativa al origen de datos en lugar de tener que especificar la ruta completa.  
  
La ubicación física a la que apunta `DataDirectory` depende del tipo de aplicación. En este ejemplo, el archivo Northwind.mdf que se va a adjuntar se encuentra en la carpeta \app_data de la aplicación.  
  
```console
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;  
AttachDBFilename=|DataDirectory|\app_data\Northwind.mdf;  
Initial Catalog=Northwind;  
```  
  
Cuando se utiliza `DataDirectory`, la ruta de acceso del archivo resultante no puede ser superior en la estructura de directorios que el directorio al que apunta la cadena de sustitución. Por ejemplo, si la propiedad `DataDirectory` totalmente expandida es C:\AppDirectory\app_data, la cadena de conexión de ejemplo que se muestra arriba funciona porque está por debajo de c:\AppDirectory. Pero si se intenta especificar `DataDirectory` como `|DataDirectory|\..\data`, se produce un error porque \data no es un subdirectorio de \AppDirectory.  
  
Si la cadena de conexión tiene una cadena de sustitución con formato incorrecto, se producirá <xref:System.ArgumentException>.  
  
> [!NOTE]
>  <xref:Microsoft.Data.SqlClient> resuelve las cadenas de sustitución en rutas de acceso completas en el sistema de archivos del equipo local. Por lo tanto, no se admiten los nombres de ruta de acceso UNC, HTTP y de servidor remoto. Se produce una excepción cuando se abre la conexión si el servidor no se encuentra en el equipo local.  
  
Cuando se abre <xref:Microsoft.Data.SqlClient.SqlConnection>, se redirige desde la instancia de SQL Server Express predeterminada a una instancia iniciada en el entorno de ejecución que se ejecuta en la cuenta del autor de llamada.  
  
> [!NOTE]
>  Puede que sea necesario aumentar el valor de <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionTimeout%2A>, ya que las instancias de usuario pueden tardar más tiempo en cargarse que las instancias normales.  
  
El fragmento de código siguiente se abre una nueva propiedad `SqlConnection`, se muestra la cadena de conexión en la ventana de la consola y, a continuación, se cierra la conexión al cerrar el bloque de código `using`.  
  
```csharp  
private static void OpenSqlConnection()  
{  
    // Retrieve the connection string.  
    string connectionString = GetConnectionString();  
  
    using (SqlConnection connection =   
        new SqlConnection(connectionString))  
    {  
        connection.Open();  
        Console.WriteLine("ConnectionString: {0}",   
             connection.ConnectionString);  
    }  
}  
```  
  
> [!NOTE]
>  Las instancias de usuario no se admiten en el código de Common Language Runtime (CLR) que se ejecuta dentro de SQL Server. Se produce <xref:System.InvalidOperationException> si se llama a `Open` en una propiedad <xref:Microsoft.Data.SqlClient.SqlConnection> que tiene `User Instance=true` en la cadena de conexión.  
  
## <a name="lifetime-of-a-user-instance-connection"></a>Duración de una conexión de instancia de usuario  
A diferencia de las versiones de SQL Server que se ejecutan como un servicio, no es necesario iniciar y detener manualmente las instancias de SQL Server Express. Cada vez que un usuario inicia sesión y se conecta a una instancia de usuario, la instancia de usuario se inicia si aún no se está ejecutando. Las bases de datos de instancia de usuario tienen la opción `AutoClose` establecida de modo que la base de datos se cierre automáticamente después de un período de inactividad. El proceso Sqlservr.exe que se inicia se mantiene en ejecución durante un período de tiempo de espera limitado después de cerrarse la última conexión a la instancia, por lo que no es necesario reiniciarlo si se abre otra conexión antes de que expire el tiempo de espera. La instancia de usuario se cierra automáticamente si no se abre ninguna conexión nueva antes de que haya expirado el período de tiempo de espera. Un administrador del sistema en la instancia principal puede establecer la duración del período de espera de una instancia de usuario mediante **sp_configure** para cambiar la opción **user instance timeout**. El valor predeterminado es 60 minutos.  
  
> [!NOTE]
>  Si se usa `Min Pool Size` en la cadena de conexión con un valor mayor que cero, el agrupador de conexiones mantendrá siempre algunas conexiones abiertas y la instancia de usuario no se cerrará automáticamente.  
  
## <a name="how-user-instances-work"></a>Funcionamiento de las instancias de usuario  
La primera vez que se genera una instancia de usuario para cada usuario, las bases de datos del sistema **master** y **msdb** se copian desde la carpeta Template Data en una ruta de acceso en el directorio del repositorio de datos de aplicación local del usuario para que las use exclusivamente la instancia de usuario. La ruta de acceso es normalmente `C:\Documents and Settings\<UserName>\Local Settings\Application Data\Microsoft\Microsoft SQL Server Data\SQLEXPRESS`. Cuando se inicia una instancia de usuario, también se escriben en este directorio el registro **tempdb** y los archivos de seguimiento. Se genera un nombre para la instancia, que se garantiza que sea único para cada usuario.  
  
De forma predeterminada, a todos los miembros del grupo Windows Builtin\Users se les conceden permisos para conectarse en la instancia local, así como permisos de lectura y ejecución en los archivos binarios de SQL Server. Una vez comprobadas las credenciales del usuario que realiza la llamada y hospeda la instancia de usuario, ese usuario se convierte en `sysadmin` en esa instancia. Solo la memoria compartida está habilitada para las instancias de usuario, lo que significa que solo se pueden realizar operaciones en el equipo local.  
  
A los usuarios se les deben conceder permisos de lectura y escritura en los archivos .mdf y. ldf especificados en la cadena de conexión.  
  
> [!NOTE]
>  Los archivos .mdf y. ldf representan los archivos de base de datos y de registro, respectivamente. Estos dos archivos son conjuntos coincidentes, por lo que se debe tener cuidado durante las operaciones de copia de seguridad y restauración. El archivo de base de datos contiene información acerca de la versión exacta del archivo de registro y la base de datos no se abrirá si está unida a un archivo de registro incorrecto.  
  
Para evitar daños en los datos, se abre una base de datos en la instancia de usuario con acceso exclusivo. Si dos instancias de usuario diferentes comparten la misma base de datos en el mismo equipo, el usuario de la primera instancia debe cerrar la base de datos para que se pueda abrir en una segunda instancia.  
  
## <a name="user-instance-scenarios"></a>Escenarios de instancias de usuario  
Las instancias de usuario proporcionan a los desarrolladores de aplicaciones de base de datos un almacén de datos de SQL Server que no depende de que los desarrolladores tengan cuentas administrativas en sus equipos de desarrollo. Las instancias de usuario se basan en el modelo Access/Jet, donde la aplicación de base de datos simplemente se conecta a un archivo y el usuario tiene permisos totales en todos los objetos de la base de datos sin necesidad de la intervención de un administrador del sistema para conceder permisos. Está pensado para funcionar en situaciones en las que el usuario se ejecuta con una cuenta de usuario con privilegios mínimos (LUA) y no tiene privilegios administrativos en el servidor o en el equipo local, pero tiene que crear objetos y aplicaciones de base de datos. Las instancias de usuario permiten a los usuarios crear instancias en el entorno de ejecución que se ejecutan en el propio contexto de seguridad del usuario y no en el contexto de seguridad de un servicio de sistema con más privilegios.  
  
> [!IMPORTANT]
>  Las instancias de usuario solo se deben usar en escenarios en los que todas las aplicaciones que la usan sean de plena confianza.  
  
Entre los escenarios de instancias de usuario están los siguientes:  
  
- Cualquier aplicación de usuario único en la que no es necesario compartir datos.  
  
- Implementación ClickOnce. Si .NET Framework 2.0 (o posterior) o .NET Core 1.0 (o posterior) y SQL Server Express ya están instalados en el equipo de destino, los usuarios que no sean administradores pueden instalar y usar el paquete de instalación descargado como resultado de una acción ClickOnce. Tenga en cuenta que un administrador debe instalar SQL Server Express si forma parte de la configuración. Para obtener más información, consulte [Implementación de ClickOnce para formularios Windows Forms](https://docs.microsoft.com/dotnet/framework/winforms/clickonce-deployment-for-windows-forms).
  
- Hospedaje de ASP.NET dedicado mediante la autenticación de Windows. Una única instancia de SQL Server Express se puede hospedar en una intranet. La aplicación se conecta mediante la cuenta de Windows ASPNET, no mediante la suplantación. Las instancias de usuario no deben usarse para escenarios de hospedaje compartido o de terceros en los que todas las aplicaciones compartan la misma instancia de usuario y ya no permanezcan aisladas entre sí.  
  
## <a name="next-steps"></a>Pasos siguientes
- [SQL Server y ADO.NET](index.md)
