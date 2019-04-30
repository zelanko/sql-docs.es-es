---
title: Referencia de API de instancia de SQL Server Express LocalDB | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: faec46da-0536-4de3-96f3-83e607c8a8b6
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: adfddc5de02f13b592b1f03107a67c4a3c449d0c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63128638"
---
# <a name="sql-server-express-localdb-instance-api-reference"></a>Referencia de la API de instancia de SQL Server Express LocalDB
  En el mundo tradicional de SQL Server basado en servicios, las instancias de SQL Server individuales que están instaladas en un equipo único se encuentran físicamente separadas; es decir, cada instancia debe instalarse y quitarse de forma individual, tener un conjunto independiente de archivos binarios y ejecutarse en un proceso individual del servicio. El nombre de la instancia de SQL Server se utiliza para especificar a qué instancia de SQL Server se desea conectar el usuario.  
  
 La API de la instancia de SQL Server Express LocalDB usa un modelo de instancia simplificado y "light". Aunque las instancias individuales de LocalDB estén separadas en el disco y en el Registro, utilizan el mismo conjunto de archivos binarios compartidos de LocalDB. Además, LocalDB no utiliza servicios; las instancias de LocalDB se inician a petición a través de llamadas a la API de la instancia de LocalDB. En LocalDB, el nombre de instancia se utiliza para especificar la instancia de LocalDB con la que va a trabar el usuario.  
  
 Una instancia de LocalDB siempre pertenece a un único usuario y es visible y accesible solo desde el contexto de este usuario, a menos que el uso compartido de la instancia está habilitado.  
  
 Aunque técnicamente las instancias de LocalDB no son las mismas que las instancias tradicionales de SQL Server, el uso al que están dirigidas es similar. Se denominan *instancias* para resaltar esta similitud y para que resulten más intuitivas para los usuarios de SQL Server.  
  
 LocalDB admite dos tipos de instancias: instancias automáticas (AI) e instancias con nombre (NI). El identificador para una instancia de LocalDB es el nombre de instancia.  
  
## <a name="automatic-localdb-instances"></a>Instancias automáticas de LocalDB  
 Instancias automáticas de LocalDB son "públicas"; se crean y administran automáticamente para el usuario y se puede usar cualquier aplicación. Existe una instancia de LocalDB automática para todas las versiones de LocalDB que se instala en el equipo del usuario.  
  
 Las instancias automáticas de LocalDB proporcionan una administración agilizada de la instancia. El usuario no necesita crear la instancia. De esta forma, los usuarios pueden instalar aplicaciones con facilidad y migrarlas a equipos diferentes. Si el equipo de destino tiene la versión especificada de LocalDB instalada, la instancia automática de LocalDB de esa versión también estará disponible en ese equipo.  
  
### <a name="automatic-instance-management"></a>Administración de instancias automáticas  
 Los usuarios no necesitan crear una instancia automática de LocalDB. La instancia se crea de forma diferida la primera vez que se usa la instancia, siempre que la versión especificada de LocalDB está disponible en el equipo del usuario. Desde el punto de vista del usuario, la instancia automática siempre está presente si los archivos binarios de LocalDB están presentes.  
  
 En las instancias automáticas están también operativas otras operaciones de administración de estancias, como Eliminar, Compartir y No compartir. Concretamente, al eliminar una instancia automática, se restablece la instancia de forma eficaz, la cual se creará en la próxima operación de inicio. Es posible que sea necesario eliminar una instancia automática si se dañan las bases de datos del sistema.  
  
### <a name="automatic-instance-naming-rules"></a>Normas de nomenclatura para instancias automáticas  
 Las instancias automáticas de LocalDB cuentan con un patrón especial para el nombre de instancia que pertenece a un espacio de nombres reservado. Esto es necesario para evitar conflictos de nombres con las instancias con nombre de LocalDB.  
  
 El nombre de instancia automática es el número de versión de versión de línea de base de LocalDB precedido por un carácter único "v". Esto es similar a "v" más dos números con un período entre ellos; Por ejemplo, v11.0 o V12.00.  
  
 Entre los ejemplos de nombre de instancia incorrectos, se encuentran:  
  
-   11.0 (falta el carácter "v" al principio)  
  
-   v11 (falta un punto y una segunda cifra de versión)  
  
-   v11. (falta el segundo número de la versión)  
  
-   v11.0.1.2 (el número de versión tiene más de dos porciones)  
  
## <a name="named-localdb-instances"></a>Instancias con nombre de LocalDB  
 Las instancias con nombre de LocalDB son "privadas"; una instancia pertenece a una sola aplicación que se encarga de crear y administrar la instancia. Las instancias con nombre de LocalDB proporcionan aislamiento y mejoran el rendimiento.  
  
### <a name="named-instance-creation"></a>Creación de instancias con nombre  
 El usuario debe crear las instancias con nombre explícitamente a través de la API de administración de LocalDB o implícitamente a través del archivo app.config para una aplicación administrada. Las aplicaciones administradas también pueden utilizar la API.  
  
 Cada instancia con nombre tiene una versión de LocalDB asociada; es decir, señala a un conjunto de archivos binarios de LocalDB determinado. La versión de la instancia con nombre se establece durante el proceso de creación de la instancia.  
  
### <a name="named-instance-naming-rules"></a>Normas de nomenclatura para instancias con nombre  
 Los nombres de instancia de LocalDB pueden tener un total de hasta 128 caracteres (el límite queda establecido según el tipo de datos de `sysname`). Se trata de una importante diferencia si se compara con los nombres tradicionales de instancia de SQL Server, las cuales están limitadas a los nombres de NetBIOS de 16 caracteres ASCII. El motivo de esta diferencia es que LocalDB trata las bases de datos como archivos y, por lo tanto, implica una semántica basada en archivos, por lo que es intuitivo para los usuarios tengan más libertad de elegir los nombres de instancia.  
  
 Los nombres de instancia de LocalDB pueden contener cualquier tipo de caracteres Unicode que sean válidos en el componente de nombre de archivo. Caracteres no válidos en un componente de nombre de archivo, generalmente, incluyen los siguientes caracteres: Caracteres ASCII/Unicode 1 31 a través, así como comillas dobles ("), menor que (\<), mayor que (>), barra vertical (|), retroceso (\b), tabulación (\t), dos puntos (:), asterisco (*), signo de interrogación (?), barra diagonal inversa (\\) y la barra diagonal (/). Tenga en cuenta que el carácter NULL (\0) está permitido porque se utiliza para la terminación de cadenas; se ignorará todo aquello que esté tras el carácter NULL.  
  
> [!NOTE]  
>  La lista de caracteres no válidos puede depender del sistema operativo y podría cambiar en versiones futuras.  
  
 Los espacios en blanco iniciales y finales en los nombres de instancia se omiten y se recortarán.  
  
 Para evitar conflictos de nomenclatura, denominados LocalDB instancias no pueden tener un nombre que sigue el patrón de nomenclatura para instancias automáticas, como se describió anteriormente en "Reglas de nomenclatura de instancia automática". Un intento de crear una instancia con nombre con un nombre que sigue el patrón de nomenclatura de la instancia automática de forma eficaz, crea una instancia predeterminada.  
  
## <a name="sql-server-express-localdb-reference-topics"></a>Temas de referencia de SQL Server Express LocalDB  
 [Información de encabezado y versión de SQL Server Express LocalDB](sql-server-express-localdb-header-and-version-information.md)  
 Proporciona información sobre el archivo del encabezado y las claves del Registro para encontrar la API de la instancia de LocalDB.  
  
 [Herramienta de administración de línea de comandos: SqlLocalDB.exe](command-line-management-tool-sqllocaldb-exe.md)  
 Describe SqlLocalDB.exe, una herramienta para administrar las instancias de LocalDB desde la línea de comandos.  
  
 [Función LocalDBCreateInstance](localdbcreateinstance-function.md)  
 Describe la función para crear una nueva instancia de LocalDB.  
  
 [Función LocalDBDeleteInstance](localdbdeleteinstance-function.md)  
 Describe la función para quitar una instancia de LocalDB.  
  
 [Función LocalDBFormatMessage](localdbformatmessage-function.md)  
 Describe la función para devolver la descripción localizada para un error de LocalDB.  
  
 [Función LocalDBGetInstanceInfo](localdbgetinstanceinfo-function.md)  
 Describe características para obtener información de una instancia de LocalDB, como si esta existe, información de versión, si se está ejecutando, etc.  
  
 [Función LocalDBGetInstances](localdbgetinstances-function.md)  
 Describe la función para devolver todas las instancias de LocalDB con una versión determinada.  
  
 [Función LocalDBGetVersionInfo](localdbgetversioninfo-function.md)  
 Describe la función para devolver información de una versión concreta de LocalDB.  
  
 [Función LocalDBGetVersions](localdbgetversions-function.md)  
 Describe la función para devolver todas las versiones de LocalDB disponibles en un equipo.  
  
 [Función LocalDBShareInstance](localdbshareinstance-function.md)  
 Describe la función para compartir una instancia especificada de LocalDB.  
  
 [Función LocalDBStartInstance](localdbstartinstance-function.md)  
 Describe la función para iniciar una instancia especificada de LocalDB.  
  
 [Función LocalDBStartTracing](localdbstarttracing-function.md)  
 Describe la función para habilitar el seguimiento de API para un usuario.  
  
 [Función LocalDBStopInstance](localdbstopinstance-function.md)  
 Describe la función para detener la ejecución de una instancia determinada de LocalDB.  
  
 [Función LocalDBStopTracing](localdbstoptracing-function.md)  
 Describe la función para deshabilitar el seguimiento de API para un usuario.  
  
 [Función LocalDBUnshareInstance](localdbunshareinstance-function.md)  
 Describe la función para detener el uso compartido de una instancia determinada de LocalDB.  
  
  
