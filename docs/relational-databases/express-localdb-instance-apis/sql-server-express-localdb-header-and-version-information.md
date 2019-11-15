---
title: SQL Server Express encabezado de LocalDB & información de versión
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apilocation:
- sqluserinstance.dll
ms.assetid: 506b5161-b902-4894-b87b-9192d7b1664a
author: CarlRabeler
ms.author: carlrab
ms.custom: seo-dt-2019
ms.openlocfilehash: f5aeb8a5eda8e4e49e478cbc53cd0ad90e3cc890
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095475"
---
# <a name="sql-server-express-localdb-header-and-version-information"></a>Información de encabezado y versión de SQL Server Express LocalDB
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  No hay ningún archivo de encabezado independiente para la API de instancia de SQL Server Express LocalDB; las firmas de función y los códigos de error de LocalDB se definen en el archivo de encabezado de SQL Server Native Client (sqlncli.h). Para utilizar la instancia API de LocalDB, debe incluir el archivo de encabezado sqlncli.h en el proyecto.  
  
## <a name="localdb-versioning"></a>Versión de LocalDB  
 La instalación de LocalDB utiliza un conjunto único de archivos binarios por versión principal de SQL Server. Estas versiones de LocalDB se mantienen y se revisan de forma independiente. Esto significa que el usuario tiene que especificar la versión de línea base de LocalDB (es decir, la versión principal de SQL Server) que se va a utilizar. La versión se especifica en el formato de versión estándar definido por la clase .NET Framework **System. version** :  
  
 *major.minor[.build[.revision]]*  
  
 Los dos primeros números de la cadena de versión (*principal* y *secundaria*) son obligatorios. Los dos últimos números en la cadena de versión (*compilación* y *revisión*) son opcionales y tienen como valor predeterminado cero si el usuario los deja fuera. Esto significa que si el usuario especifica solo "12,2" como número de versión de LocalDB, se tratará como si el usuario hubiera especificado "12.2.0.0".  
  
 La versión para la instalación de LocalDB se define en la clave del Registro MSSQLServer\CurrentVersion en la clave del Registro de la instancia de SQL Server, por ejemplo:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL13E.LOCALDB\ MSSQLServer\CurrentVersion: "CurrentVersion"="12.0.2531.0"  
```  
  
 Si hay varias versiones de LocalDB en la misma estación de trabajo, se admiten en paralelo. Sin embargo, el código de usuario siempre usa la dll de **SQLUserInstance** disponible más reciente en el equipo local para conectarse a las instancias de LocalDB.  
  
## <a name="locating-the-sqluserinstance-dll"></a>Localizar la DLL de SQLUserInstance  
 Para buscar el archivo dll de **SQLUserInstance** , el proveedor de cliente utiliza la siguiente clave del registro:  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions]  
```  
  
 En esta clave hay una lista de claves, una para cada versión de LocalDB que se haya instalado en el equipo. Cada una de estas claves se denomina con el número de versión de LocalDB en el formato *\<> de versión principal*. *\<> de versión secundaria* (por ejemplo, la clave de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] se denomina 13,0). En cada clave de la versión hay un par nombre-valor `InstanceAPIPath` que definen la ruta completa al archivo SQLUserInstance.dll que se haya instalado con esa versión. En el ejemplo siguiente se muestran las entradas del registro para un equipo que tiene instaladas las versiones 11,0 y 13,0 de LocalDB:  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions\13.0]  
"InstanceAPIPath"="C:\\Program Files\\Microsoft SQL Server\\130\\LocalDB\\Binn\\SqlUserInstance.dll"  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions\13.0]  
"InstanceAPIPath"="C:\\Program Files\\Microsoft SQL Server\\130\\LocalDB\\Binn\\SqlUserInstance.dll"]  
```  
  
 El proveedor de cliente debe encontrar la última versión entre todas las versiones instaladas y cargar el archivo dll de **SQLUserInstance** del valor de `InstanceAPIPath` asociado.  
  
### <a name="wow64-mode-on-64-bit-windows"></a>Modo WOW64 en Windows de 64 bits  
 Las instalaciones de 64 bits de LocalDB tendrán un conjunto adicional de claves del Registro para que las aplicaciones de 32 bits que se ejecutan en el modo de Windows de 32 bits sobre Windows de 64 bits (WOW64) puedan utilizar LocalDB. Concretamente, en Windows de 64 bits, el MSI de LocalDB creará las claves del Registro siguientes:  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Wow6432Node\Microsoft SQL Server Local DB\Installed Versions\13.0]  
"InstanceAPIPath"="C:\\Program Files (x86)\\Microsoft SQL Server\\130\\LocalDB\\Binn\\SqlUserInstance.dll"  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Wow6432Node\Microsoft SQL Server Local DB\Installed Versions\13.0]  
"InstanceAPIPath"="C:\\Program Files (x86)\\Microsoft SQL Server\\130\\LocalDB\\Binn\\SqlUserInstance.dll"]  
  
```  
  
 los programas de 64 bits que leen la clave de `Installed Versions` verán valores que señalan a versiones de 64 bits de la dll de **SQLUserInstance** , mientras que los programas de 32 bits (que se ejecutan en Windows de 64 bits en modo WOW64) se redirigirán automáticamente a una clave de `Installed Versions` ubicada en el `Wow6432Node` Hive. Esta clave contiene valores que apuntan a las versiones de 32 bits de la dll de **SQLUserInstance** .  
  
## <a name="using-localdb_define_proxy_functions"></a>Uso de LOCALDB_DEFINE_PROXY_FUNCTIONS  
 La API de instancia de LocalDB define una constante denominada LOCALDB_DEFINE_PROXY_FUNCTIONS que automatiza la detección y carga de la dll de **SqlUserInstance** .  
  
 La sección de código que se habilita a través de esta constante proporciona una implementación de servidores proxy para cada una de las API de LocalDB. Las implementaciones de proxy usan una función común para enlazar con los puntos de entrada del archivo dll de **SqlUserInstance** instalado más reciente y, a continuación, reenviar las solicitudes.  
  
 Se habilitan las características del servidor proxy únicamente si la constante LOCALDB_DEFINE_PROXY_FUNCTIONS se ha definido en el código de usuario antes de incluir el archivo sqlncli.h. La constante debe estar definida en tan solo un módulo de origen (archivo .cpp) porque define los nombres de función externa para todos los puntos de entrada de la API. Proporciona una implementación de servidores proxy para cada una de las API de LocalDB.  
  
 El ejemplo de código siguiente muestra cómo utilizar la macro a partir de código C++ nativo:  
  
```  
// Define the LOCALDB_DEFINE_PROXY_FUNCTIONS constant to enable the LocalDB proxy functions   
// The #define has to take place BEFORE the API header file (sqlncli.h) is included  
#define LOCALDB_DEFINE_PROXY_FUNCTIONS  
#include <sqlncli.h>  
...  
HRESULT hr = S_OK;  
  
// Create LocalDB instance by calling the create API proxy function included by macro  
if (FAILED(hr = LocalDBCreateInstance( L"12.0", L"name", 0)))  
{  
...  
}  
...  
  
```  
  
  
