---
title: Tutorial de ciencia de datos de extremo a otro para R y SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 3d4f38fd424c881392d48b0a6a24feb7f7e27ee0
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086507"
---
# <a name="end-to-end-data-science-walkthrough-for-r-and-sql-server"></a>Tutorial de ciencia de datos de extremo a otro para R y SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este tutorial, desarrollará una solución de extremo a otro para el modelado de predicción según la compatibilidad de características de R en SQL Server 2016 o SQL Server 2017.

Este tutorial se basa en un conjunto de datos público conocido, el conjunto de datos de los taxis de Nueva York. Usar una combinación de código de R, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos y funciones SQL personalizadas para crear un modelo de clasificación que indique la probabilidad de que el controlador es posible que reciba una propina en una carrera de taxi determinado. También implementa el modelo R [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y usar los datos del servidor para generar puntuaciones según el modelo.

En este ejemplo se puede extender a todos los tipos de problemas de la vida real, como predecir las respuestas de clientes en las campañas de ventas o predecir los gastos adicionales o asistencia en eventos. Dado que el modelo se puede invocar desde un procedimiento almacenado, puede insertar fácilmente en una aplicación.

Dado que el tutorial está diseñado para presentar a los desarrolladores de R [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], se usa R siempre que sea posible. Sin embargo, esto no significa que R sea necesariamente la mejor herramienta para cada tarea. En muchos casos, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podría proporcionar un mejor rendimiento, especialmente en tareas como la agregación de datos e ingeniería de características.  Esas tareas pueden beneficiarse de las nuevas características de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], como los índices de almacén de columnas con optimización para memoria. Intentamos señalar posibles optimizaciones en el camino.

## <a name="target-audience"></a>Audiencia de destino

Este tutorial está pensado para desarrolladores de R o SQL. Proporciona una introducción a cómo se puede integrar R en flujos de trabajo empresariales mediante [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].  Debe estar familiarizado con operaciones de base de datos, como la creación de tablas y bases de datos, importación de datos y ejecutar consultas.

+ Se incluyen todos los scripts SQL y R.
+ Es posible que deba modificar las cadenas en los scripts se ejecuten en su entorno. Puede hacerlo con cualquier editor de código, como [Visual Studio Code](https://code.visualstudio.com/Download).

## <a name="prerequisites"></a>Requisitos previos

Se recomienda que realice este tutorial en un equipo portátil o en otro equipo que tenga instaladas las bibliotecas de Microsoft R. Debe ser capaz de conectarse, en la misma red, a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equipo con SQL Server y el lenguaje R habilitado.

Puede ejecutar el tutorial en un equipo que tenga tanto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y un entorno de desarrollo de R pero no se recomienda esta configuración para un entorno de producción.

Si desea ejecutar comandos de R desde un equipo remoto, como un equipo portátil o en otro equipo en red, debe instalar las bibliotecas de Microsoft R Open. Puede instalar Microsoft R Client o Microsoft R Server. El equipo remoto debe ser capaz de conectarse a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia.

Si tiene que colocar el cliente y servidor en el mismo equipo, asegúrese de instalar un conjunto independiente de bibliotecas de R de Microsoft para su uso en el envío de script de R desde un cliente "remoto". No utilice las bibliotecas de R que se instalan para su uso por la instancia de SQL Server para este propósito.

## <a name="add-r-to-sql-server"></a>Agregar R a SQL Server

Debe tener acceso a una instancia de SQL Server compatible con R instalado. Este tutorial originalmente se desarrolló para el servidor SQL 2016 y probado en 2017, por lo que podrá utilizar cualquiera de las siguientes versiones de SQL Server. (Hay algunas pequeñas diferencias en las funciones de RevoScaleR entre las versiones).

+ [Instalar SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)
+ [Instalar SQL Server 2016 R Services](../install/sql-r-services-windows-install.md).

## <a name="install-an-r-development-environment"></a>Instalar un entorno de desarrollo de R

En este tutorial, se recomienda que use un entorno de desarrollo de R. Estas son algunas sugerencias:

- **Herramientas de R para Visual Studio** (RTVS) es un complemento gratuito complemento que proporciona Intellisense, depuración y la compatibilidad con Microsoft R. se puede usar con R Server y SQL Server Machine Learning Services. Para descargarlo, consulte la página sobre [Herramientas de R para Visual Studio](https://www.visualstudio.com/vs/rtvs/).

- **Microsoft R Client** es una herramienta de desarrollo ligera que admite el desarrollo en R mediante el paquete RevoScaleR. Para obtenerla, consulte [Get Started with Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)(Introducción a Cliente de Microsoft R).

- **RStudio** es uno de los entornos de desarrollo de R más populares. Para obtener más información, consulte [ https://www.rstudio.com/products/RStudio/ ](https://www.rstudio.com/products/RStudio/).

    No se puede completar este tutorial con una instalación genérica de RStudio u otro entorno; También debe instalar los paquetes de R y las bibliotecas de conectividad de Microsoft R Open. Para obtener más información, consulte [Configurar un cliente de ciencia de datos](../r/set-up-a-data-science-client.md).

- Herramientas básicas de R (R.exe, RTerm.exe, RScripts.exe) también se instalan de forma predeterminada al instalar R en SQL Server o cliente de R. Si no desea instalar un IDE, puede usar estas herramientas.

## <a name="get-permissions-on-the-sql-server-instance-and-database"></a>Obtener permisos en la instancia de SQL Server y base de datos

Para conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ejecutar scripts y cargar datos, debe tener un inicio de sesión válido en el servidor de base de datos.  Puede usar un inicio de sesión de SQL o la autenticación integrada de Windows. Pida al administrador de base de datos para configurar los siguientes permisos para la cuenta, en la base de datos donde se utilice R:

- Crear bases de datos, tablas, funciones y procedimientos almacenados
- Escribir datos en tablas
- Capacidad de ejecutar el script de R (`GRANT EXECUTE ANY EXTERNAL SCRIPT to <user>`)

En este tutorial, hemos usado el inicio de sesión SQL **RTestUser**. Por lo general, se recomienda que utilice la autenticación integrada de Windows, pero usar el inicio de sesión SQL es más fácil para algunos fines de demostración.

## <a name="next-steps"></a>Pasos siguientes

[Preparar los datos de uso de PowerShell](walkthrough-prepare-the-data.md)
