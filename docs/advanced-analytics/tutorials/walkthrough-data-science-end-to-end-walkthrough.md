---
title: Tutorial para científicos de datos con el lenguaje R
description: Tutorial que muestra cómo crear una solución de R de un extremo a otro para el análisis en bases de datos.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/11/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ad7f5a500f740e4a302f814ec9523dfb33ecc68b
ms.sourcegitcommit: 710d60e7974e2c4c52aebe36fceb6e2bbd52727c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/11/2019
ms.locfileid: "72278275"
---
# <a name="tutorial-sql-development-for-r-data-scientists"></a>Tutorial: Desarrollo de SQL para científicos de datos de R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este tutorial para científicos de datos, aprenderá a crear una solución de un extremo a otro para el modelado predictivo basado en la compatibilidad con las características de R en SQL Server 2016 o SQL Server 2017. En este tutorial se usa una base de datos de [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) en SQL Server. 

Se usa una combinación de código R, datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y funciones SQL personalizadas para crear un modelo de clasificación que indique la probabilidad de que el controlador obtenga una propina en un viaje de taxi determinado. También implementará el modelo de R en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y utilizará los datos del servidor para generar puntuaciones basadas en el modelo.

Este ejemplo se puede ampliar a todos los tipos de problemas de la vida real, como predecir las respuestas de los clientes a las campañas de ventas o predecir los gastos o la asistencia en los eventos. Dado que el modelo se puede invocar desde un procedimiento almacenado, se puede insertar fácilmente en una aplicación.

Dado que el tutorial está diseñado para introducir a los desarrolladores de R en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], R se usa siempre que sea posible. Sin embargo, esto no significa que R sea necesariamente la mejor herramienta para cada tarea. En muchos casos, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podría proporcionar un mejor rendimiento, especialmente en tareas como la agregación de datos e ingeniería de características.  Esas tareas pueden beneficiarse de las nuevas características de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], como los índices de almacén de columnas con optimización para memoria. Intentamos señalar posibles optimizaciones durante el proceso.

## <a name="prerequisites"></a>Requisitos previos

+ [SQL Server Machine Learning Services con la integración de r](../install/sql-machine-learning-services-windows-install.md#verify-installation) o [SQL Server r Services de 2016](../install/sql-r-services-windows-install.md)

+ [Permisos de base de datos](../security/user-permission.md) y un inicio de sesión de usuario de SQL Server Database

+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ [Base de datos de demostración de taxi de Nueva York](demo-data-nyctaxi-in-sql.md)

+ Un IDE de R como RStudio o la herramienta de RGUI integrada incluida con R

Se recomienda que realice este tutorial en una estación de trabajo cliente. Debe poder conectarse, en la misma red, a un equipo @no__t con SQL Server y el lenguaje R habilitado. Para obtener instrucciones sobre la configuración de la estación de trabajo, consulte Configuración de [un cliente de ciencia de datos para el desarrollo en R](../r/set-up-a-data-science-client.md).

Como alternativa, puede ejecutar el tutorial en un equipo que tenga [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y un entorno de desarrollo de R, pero no se recomienda esta configuración para un entorno de producción. Si necesita poner el cliente y el servidor en el mismo equipo, asegúrese de instalar un segundo conjunto de bibliotecas de Microsoft R para enviar scripts de R desde un cliente "remoto". No use las bibliotecas de R que están instaladas en los archivos de programa de la instancia de SQL Server. En concreto, si usa un equipo, necesita la biblioteca RevoScaleR en ambas ubicaciones para admitir las operaciones de cliente y de servidor.

+ C:\Archivos de Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Archivos de Programa\microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library\RevoScaleR

> [!NOTE]
> Si usa [machine learning Server](https://docs.microsoft.com/machine-learning-server/) o el [Data Science Virtual Machine](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/), en lugar de R Client, la ruta de acceso a RevoScaleR es c:\Archivos de programa\microsoft\ml Server\R_SERVER\library\RevoScaleR

<a name="add-packages"></a>

## <a name="additional-r-packages"></a>Paquetes de R adicionales

En este tutorial se requieren varias bibliotecas de R que no se instalan de forma predeterminada como parte de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Debe instalar los paquetes en el cliente en el que desarrolla la solución y en el equipo @no__t 0 donde se implementa la solución.

### <a name="on-a-client-workstation"></a>En una estación de trabajo cliente

En el entorno de R, copie las siguientes líneas y ejecute el código en una ventana de consola (Rgui o un IDE). Algunos paquetes también instalan los paquetes necesarios. En general, se instalan los paquetes 32. Para completar este paso, debe tener una conexión a Internet.
    
  ```R
  # Install required R libraries, if they are not already installed.
  if (!('ggmap' %in% rownames(installed.packages()))){install.packages('ggmap')}
  if (!('mapproj' %in% rownames(installed.packages()))){install.packages('mapproj')}
  if (!('ROCR' %in% rownames(installed.packages()))){install.packages('ROCR')}
  if (!('RODBC' %in% rownames(installed.packages()))){install.packages('RODBC')}
  ```

### <a name="on-the-server"></a>En el servidor

Tiene varias opciones para instalar paquetes en SQL Server. Por ejemplo, SQL Server proporciona una característica de [Administración de paquetes de R](../r/install-additional-r-packages-on-sql-server.md) que permite a los administradores de bases de datos crear un repositorio de paquetes y asignar a los usuarios los derechos para instalar sus propios paquetes. Sin embargo, si es administrador del equipo, puede instalar nuevos paquetes mediante R, siempre que instale en la biblioteca correcta.

> [!NOTE]
> En el servidor, **no** instale en una biblioteca de usuario aunque se le solicite. Si instala en una biblioteca de usuario, la instancia de SQL Server no puede encontrar o ejecutar los paquetes. Para obtener más información, vea [instalar nuevos paquetes de R en SQL Server](../r/install-additional-r-packages-on-sql-server.md).

1. En el equipo con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], abra RGui.exe **como administrador**.  Si ha instalado SQL Server R Services con los valores predeterminados, Rgui. exe puede encontrarse en C:\Archivos de Programa\microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\bin\x64).

2. En un símbolo del sistema de R, ejecute los siguientes comandos de R:
  
  ```R
  install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  ```
  En este ejemplo se usa la función grep de R para buscar el vector de rutas de acceso disponibles y buscar la ruta de acceso que incluye "archivos de programa". Para obtener más información, vea [https://www.rdocumentation.org/packages/base/functions/grep](https://www.rdocumentation.org/packages/base/functions/grep).

  Si cree que los paquetes ya están instalados, consulte la lista de paquetes instalados ejecutando `installed.packages()`.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Explorar y resumir los datos](walkthrough-view-and-summarize-data-using-r.md)
