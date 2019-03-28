---
title: Tutorial para científicos de datos mediante el lenguaje R - SQL Server Machine Learning
description: Tutorial que muestra cómo crear una solución de R-to-end para realizar análisis en bases de datos.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 0b1820e15975ca027af7b51e809ba920af3ffc82
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511311"
---
# <a name="tutorial-sql-development-for-r-data-scientists"></a>Tutorial: Desarrollo de SQL para científicos de datos de R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este tutorial para científicos de datos, aprenda a crear la solución de extremo a otro para el modelado de predicción según la compatibilidad de características de R en SQL Server 2016 o SQL Server 2017. Este tutorial se usa un [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) base de datos en SQL Server. 

Usar una combinación de código de R, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos y funciones SQL personalizadas para crear un modelo de clasificación que indique la probabilidad de que el controlador es posible que reciba una propina en una carrera de taxi determinado. También implementa el modelo R [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y usar los datos del servidor para generar puntuaciones según el modelo.

En este ejemplo se puede extender a todos los tipos de problemas de la vida real, como predecir las respuestas de clientes en las campañas de ventas o predecir los gastos adicionales o asistencia en eventos. Dado que el modelo se puede invocar desde un procedimiento almacenado, puede insertar fácilmente en una aplicación.

Dado que el tutorial está diseñado para presentar a los desarrolladores de R [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], se usa R siempre que sea posible. Sin embargo, esto no significa que R sea necesariamente la mejor herramienta para cada tarea. En muchos casos, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podría proporcionar un mejor rendimiento, especialmente en tareas como la agregación de datos e ingeniería de características.  Esas tareas pueden beneficiarse de las nuevas características de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], como los índices de almacén de columnas con optimización para memoria. Intentamos señalar posibles optimizaciones en el camino.

## <a name="prerequisites"></a>Requisitos previos

+ [SQL Server 2017 Machine Learning Services con integración de R](../install/sql-machine-learning-services-windows-install.md#verify-installation) o [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)

+ [Permisos de base de datos](../security/user-permission.md) y un inicio de sesión de usuario de base de datos de SQL Server

+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ [NYC Taxi demo database](demo-data-nyctaxi-in-sql.md)

+ Un IDE de R como RStudio o la herramienta RGUI integrada que se incluye con R

Se recomienda que realice este tutorial en una estación de trabajo cliente. Debe ser capaz de conectarse, en la misma red, a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equipo con SQL Server y el lenguaje R habilitado. Para obtener instrucciones sobre la configuración de la estación de trabajo, consulte [configurar un cliente de ciencia de datos para el desarrollo de R](../r/set-up-a-data-science-client.md).

Como alternativa, puede ejecutar el tutorial en un equipo que tenga tanto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y un entorno de desarrollo de R, pero no se recomienda esta configuración para un entorno de producción. Si tiene que colocar el cliente y servidor en el mismo equipo, asegúrese de instalar un segundo conjunto de bibliotecas de R de Microsoft para enviar el script de R desde un cliente "remoto". No utilice las bibliotecas de R que se instalan en los archivos de programa de la instancia de SQL Server. En concreto, si usas un equipo, necesita la biblioteca RevoScaleR de estas dos ubicaciones para admitir las operaciones de cliente y servidor.

+ C:\Program Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library\RevoScaleR

<a name="add-packages"></a>

## <a name="additional-r-packages"></a>Paquetes de R adicionales

Este tutorial requiere varias bibliotecas de R que no se instalan de forma predeterminada como parte de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Debe instalar los paquetes en el cliente donde desarrollar la solución y, en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equipo donde se implementa la solución.

### <a name="on-a-client-workstation"></a>En una estación de trabajo cliente

En el entorno de R, copie las líneas siguientes y ejecute el código en una ventana de consola (Rgui o un IDE). Algunos paquetes también instalan los paquetes necesarios. En general, unos 32 paquetes se instalan. Debe tener una conexión a internet para completar este paso.
    
  ```R
  # Install required R libraries, if they are not already installed.
  if (!('ggmap' %in% rownames(installed.packages()))){install.packages('ggmap')}
  if (!('mapproj' %in% rownames(installed.packages()))){install.packages('mapproj')}
  if (!('ROCR' %in% rownames(installed.packages()))){install.packages('ROCR')}
  if (!('RODBC' %in% rownames(installed.packages()))){install.packages('RODBC')}
  ```

### <a name="on-the-server"></a>En el servidor

Tiene varias opciones para instalar paquetes en SQL Server. Por ejemplo, SQL Server proporciona [administración de paquetes de R](../r/install-additional-r-packages-on-sql-server.md) característica que permite a los administradores de base de datos crear un repositorio de paquetes y asignarle los derechos para instalar sus propios paquetes de usuario. Sin embargo, si es administrador en el equipo, puede instalar nuevos paquetes mediante R, siempre y cuando se instala a la biblioteca correcta.

> [!NOTE]
> En el servidor, **no** instalar en una biblioteca de usuario, incluso si se le solicite. Si instala en una biblioteca de usuario, la instancia de SQL Server no puede encontrar ni ejecutar los paquetes. Para obtener más información, consulte [instalar nuevos paquetes de R en SQL Server](../r/install-additional-r-packages-on-sql-server.md).

1. En el equipo con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], abra RGui.exe **como administrador**.  Si ha instalado SQL Server R Services con los valores predeterminados, Rgui.exe puede encontrarse en C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\bin\x64).

2. En un símbolo del sistema de R, ejecute los siguientes comandos de R:
  
  ```R
  install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  ```
  Este ejemplo utiliza la función grep de R para buscar el vector de rutas de acceso disponibles y buscar la ruta de acceso que incluye "Archivos de programa". Para obtener más información, consulte [ https://www.rdocumentation.org/packages/base/functions/grep ](https://www.rdocumentation.org/packages/base/functions/grep).

  Si cree que ya están instalados los paquetes, compruebe la lista de paquetes instalados mediante la ejecución de `installed.packages()`.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Explorar y resumir los datos](walkthrough-view-and-summarize-data-using-r.md)