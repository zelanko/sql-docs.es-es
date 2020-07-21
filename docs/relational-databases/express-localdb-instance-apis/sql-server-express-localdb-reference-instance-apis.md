---
title: Referencia de la API de instancia de SQL Server Express LocalDB | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: faec46da-0536-4de3-96f3-83e607c8a8b6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2122ff4cddd045b3d73567af660ddc925d4152ee
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85767784"
---
# <a name="sql-server-express-localdb-reference---instance-apis"></a>Referencia de SQL Server Express LocalDB: API de instancia
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  En el mundo tradicional de SQL Server basado en servicios, las instancias de SQL Server individuales que están instaladas en un equipo único se encuentran físicamente separadas; es decir, cada instancia debe instalarse y quitarse de forma individual, tener un conjunto independiente de archivos binarios y ejecutarse en un proceso individual del servicio. El nombre de la instancia de SQL Server se utiliza para especificar a qué instancia de SQL Server se desea conectar el usuario.  
  
 La API de la instancia SQL Server Express LocalDB usa un modelo de instancia simplificado y "ligero". Aunque las instancias individuales de LocalDB estén separadas en el disco y en el Registro, utilizan el mismo conjunto de archivos binarios compartidos de LocalDB. Además, LocalDB no utiliza servicios; las instancias de LocalDB se inician a petición a través de llamadas a la API de la instancia de LocalDB. En LocalDB, el nombre de instancia se utiliza para especificar la instancia de LocalDB con la que va a trabar el usuario.  
  
 Una instancia de LocalDB siempre es propiedad de un solo usuario y es visible y accesible solo desde el contexto de este usuario, a menos que esté habilitado el uso compartido de la instancia.  
  
 Aunque técnicamente las instancias de LocalDB no son las mismas que las instancias tradicionales de SQL Server, el uso al que están dirigidas es similar. Se denominan *instancias* para destacar esta similitud y para que sean más intuitivas para SQL Server usuarios.  
  
 LocalDB admite dos tipos de instancias: instancias automáticas (AI) e instancias con nombre (NI). El identificador para una instancia de LocalDB es el nombre de instancia.  
  
## <a name="automatic-localdb-instances"></a>Instancias automáticas de LocalDB  
 Las instancias automáticas de LocalDB son "públicas"; se crean y se administran automáticamente para el usuario y se pueden usar en cualquier aplicación. Existe una instancia automática de LocalDB para cada versión de LocalDB instalada en el equipo del usuario.  
  
 Las instancias automáticas de LocalDB proporcionan una administración agilizada de la instancia. El usuario no necesita crear la instancia. De esta forma, los usuarios pueden instalar aplicaciones con facilidad y migrarlas a equipos diferentes. Si el equipo de destino tiene la versión especificada de LocalDB instalada, la instancia automática de LocalDB de esa versión también estará disponible en ese equipo.  
  
### <a name="automatic-instance-management"></a>Administración de instancias automáticas  
 Los usuarios no necesitan crear una instancia automática de LocalDB. La instancia se crea de forma diferida la primera vez que se usa la instancia, siempre que la versión especificada de LocalDB esté disponible en el equipo del usuario. Desde el punto de vista del usuario, la instancia automática siempre está presente si los archivos binarios de LocalDB están presentes.  
  
 En las instancias automáticas están también operativas otras operaciones de administración de estancias, como Eliminar, Compartir y No compartir. Concretamente, al eliminar una instancia automática, se restablece la instancia de forma eficaz, la cual se creará en la próxima operación de inicio. Es posible que sea necesario eliminar una instancia automática si se dañan las bases de datos del sistema.  
  
### <a name="automatic-instance-naming-rules"></a>Normas de nomenclatura para instancias automáticas  
 Las instancias automáticas de LocalDB cuentan con un patrón especial para el nombre de instancia que pertenece a un espacio de nombres reservado. Esto es necesario para evitar conflictos de nombres con las instancias con nombre de LocalDB.  
  
 El nombre de instancia automática es el número de versión de la versión de línea base de LocalDB precedido por un solo carácter "v". Es similar a "v" más dos números con un punto entre ellos; por ejemplo, v 11.0 o V 12,00.  
  
 Entre los ejemplos de nombre de instancia incorrectos, se encuentran:  
  
-   11,0 (falta el carácter "v" al principio)  
  
-   v11 (falta un punto y una segunda cifra de versión)  
  
-   v11. (falta el segundo número de la versión)  
  
-   v11.0.1.2 (el número de versión tiene más de dos porciones)  
  
## <a name="named-localdb-instances"></a>Instancias con nombre de LocalDB  
 Las instancias con nombre de LocalDB son "privadas"; una instancia es propiedad de una sola aplicación que es responsable de la creación y administración de la instancia. Las instancias con nombre de LocalDB proporcionan aislamiento y mejoran el rendimiento.  
  
### <a name="named-instance-creation"></a>Creación de instancias con nombre  
 El usuario debe crear las instancias con nombre explícitamente a través de la API de administración de LocalDB o implícitamente a través del archivo app.config para una aplicación administrada. Las aplicaciones administradas también pueden utilizar la API.  
  
 Cada instancia con nombre tiene una versión de LocalDB asociada; es decir, señala a un conjunto de archivos binarios de LocalDB determinado. La versión de la instancia con nombre se establece durante el proceso de creación de la instancia.  
  
### <a name="named-instance-naming-rules"></a>Normas de nomenclatura para instancias con nombre  
 Un nombre de instancia de LocalDB puede tener hasta un total de 128 caracteres (el límite se impone mediante el tipo de datos **sysname** ). Se trata de una importante diferencia si se compara con los nombres tradicionales de instancia de SQL Server, las cuales están limitadas a los nombres de NetBIOS de 16 caracteres ASCII. La razón de esta diferencia es que LocalDB trata las bases de datos como archivos y, por tanto, implica la semántica basada en archivos, por lo que es intuitivo que los usuarios tengan más libertad para elegir los nombres de instancia.  
  
 Los nombres de instancia de LocalDB pueden contener cualquier tipo de caracteres Unicode que sean válidos en el componente de nombre de archivo. Los caracteres no válidos en un componente FILENAME suelen incluir los siguientes caracteres: caracteres ASCII/Unicode 1 a 31, así como comillas ("), menor que ( \<), greater than (> ), barra vertical (|), retroceso (\b), tabulación (\t), dos puntos (:), asterisco (*), signo de interrogación (?), barra diagonal inversa ( \\ ) Tenga en cuenta que el carácter NULL (\0) está permitido porque se utiliza para la terminación de cadenas; se ignorará todo aquello que esté tras el carácter NULL.  
  
> [!NOTE]  
>  La lista de caracteres no válidos puede depender del sistema operativo y podría cambiar en versiones futuras.  
  
 Los espacios en blanco iniciales y finales en los nombres de instancia se omiten y se recortarán.  
  
 Para evitar conflictos de nombres, las instancias de LocalDB con nombre no pueden tener un nombre que siga el patrón de nomenclatura para las instancias automáticas, tal y como se describió anteriormente en "reglas de nomenclatura de instancia automática". Un intento de crear una instancia con nombre con un nombre que sigue el patrón de nomenclatura de instancia automática crea eficazmente una instancia predeterminada.  
  
## <a name="sql-server-express-localdb-reference-topics"></a>Temas de referencia de SQL Server Express LocalDB  
 [Información de encabezado y versión de SQL Server Express LocalDB](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
 Proporciona información sobre el archivo del encabezado y las claves del Registro para encontrar la API de la instancia de LocalDB.  
  
 [Herramienta de administración de la línea de comandos: SqlLocalDB.exe](../../relational-databases/express-localdb-instance-apis/command-line-management-tool-sqllocaldb-exe.md)  
 Describe SqlLocalDB.exe, una herramienta para administrar las instancias de LocalDB desde la línea de comandos.  
  
 [Función LocalDBCreateInstance](../../relational-databases/express-localdb-instance-apis/localdbcreateinstance-function.md)  
 Describe la función para crear una nueva instancia de LocalDB.  
  
 [Función LocalDBDeleteInstance](../../relational-databases/express-localdb-instance-apis/localdbdeleteinstance-function.md)  
 Describe la función para quitar una instancia de LocalDB.  
  
 [Función LocalDBFormatMessage](../../relational-databases/express-localdb-instance-apis/localdbformatmessage-function.md)  
 Describe la función para devolver la descripción localizada para un error de LocalDB.  
  
 [Función LocalDBGetInstanceInfo](../../relational-databases/express-localdb-instance-apis/localdbgetinstanceinfo-function.md)  
 Describe características para obtener información de una instancia de LocalDB, como si esta existe, información de versión, si se está ejecutando, etc.  
  
 [Función LocalDBGetInstances](../../relational-databases/express-localdb-instance-apis/localdbgetinstances-function.md)  
 Describe la función para devolver todas las instancias de LocalDB con una versión determinada.  
  
 [Función LocalDBGetVersionInfo](../../relational-databases/express-localdb-instance-apis/localdbgetversioninfo-function.md)  
 Describe la función para devolver información de una versión concreta de LocalDB.  
  
 [Función LocalDBGetVersions](../../relational-databases/express-localdb-instance-apis/localdbgetversions-function.md)  
 Describe la función para devolver todas las versiones de LocalDB disponibles en un equipo.  
  
 [Función LocalDBShareInstance](../../relational-databases/express-localdb-instance-apis/localdbshareinstance-function.md)  
 Describe la función para compartir una instancia especificada de LocalDB.  
  
 [Función LocalDBStartInstance](../../relational-databases/express-localdb-instance-apis/localdbstartinstance-function.md)  
 Describe la función para iniciar una instancia especificada de LocalDB.  
  
 [Función LocalDBStartTracing](../../relational-databases/express-localdb-instance-apis/localdbstarttracing-function.md)  
 Describe la función para habilitar el seguimiento de API para un usuario.  
  
 [Función LocalDBStopInstance](../../relational-databases/express-localdb-instance-apis/localdbstopinstance-function.md)  
 Describe la función para detener la ejecución de una instancia determinada de LocalDB.  
  
 [Función LocalDBStopTracing](../../relational-databases/express-localdb-instance-apis/localdbstoptracing-function.md)  
 Describe la función para deshabilitar el seguimiento de API para un usuario.  
  
 [Función LocalDBUnshareInstance](../../relational-databases/express-localdb-instance-apis/localdbunshareinstance-function.md)  
 Describe la función para detener el uso compartido de una instancia determinada de LocalDB.  
  
  
