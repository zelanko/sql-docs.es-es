---
title: "Preguntas más frecuentes de actualización e instalación para el aprendizaje automático de SQL Server | Documentos de Microsoft"
ms.date: 10/31/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 001e66b9-6c3f-41b3-81b7-46541e15f9ea
caps.latest.revision: "59"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: f0c6aac38001506b51ff7d14307f23b461334eb7
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2017
---
# <a name="upgrade-and-installation-faq-for-sql-server-machine-learning"></a>Preguntas más frecuentes de actualización e instalación para el aprendizaje automático de SQL Server

Este tema proporciona respuestas a algunas preguntas comunes acerca de la instalación de características de SQL Server de aprendizaje automático. Además se ocupa de las preguntas habituales acerca de las actualizaciones.

+ Se producen algunos problemas sólo con las actualizaciones de versiones preliminares. Por lo tanto, se recomienda que identificar la versión y edición primero antes de leer estas notas.
+ Actualice a la versión más reciente o la versión de servicio tan pronto como sea posible, para resolver los problemas que se corrigieron en las versiones recientes.

**Se aplica a:** (en bases de datos) de servicios de aprendizaje de automático de SQL Server 2016 R Services, SQL Server de 2017

## <a name="performing-setup-for-the-first-time"></a>Llevar a cabo el programa de instalación para la primera vez

Siga los procedimientos para configurar [!INCLUDE[sscurrent_md](../../includes/sscurrent_md.md)] y los componentes de R, como se describe aquí: 

+ [Configurar SQL Server R Services o Machine Learning Services en bases de datos](../r/set-up-sql-server-r-services-in-database.md)
+ [Configurar SQL Server 2017 con Python](../python/setup-python-machine-learning-services.md)
+ [Crear un R Server independiente](../r/create-a-standalone-r-server.md)

> [!IMPORTANT]
> 
> Después de instalar SQL Server y la máquina de aprendizaje de las características, antes de poder usar scripts de R o Python, debe completar algunos pasos de configuración adicionales. Eso es porque la característica de ejecución de script externo no está habilitada de forma predeterminada.

### <a name="requirements-and-restrictions"></a>Requisitos y restricciones

Dependiendo de la compilación de SQL Server que va a instalar, se podrían aplicar algunas de las siguientes limitaciones:

- En las versiones anteriores de SQL Server 2016 R Services, se requería la notación de tiene el formato 8.3 en la unidad que contiene el directorio de trabajo. Si instaló una versión preliminar, la actualización a Service Pack 1 de SQL Server 2016 debe solucionar este problema. Este requisito no se aplica a las versiones después del SP1.

- Actualmente, no puede instalar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] en un clúster de conmutación por error. 

- En una máquina virtual de Azure, alguna configuración adicional puede ser necesario. Por ejemplo, deberá crear una excepción de firewall para permitir el acceso remoto.

- Instalación de en paralelo con otra versión de R, o con otras versiones de Revolution Analytics, no se admite.

- Ya no se admite la instalación nueva de ninguna versión preliminar de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] . Si está utilizando una versión preliminar, actualizar tan pronto como sea posible.

- Deshabilitar el antivirus antes de comenzar el programa de instalación. Una vez completada la instalación, se recomienda suspender la detección de virus en las carpetas usadas por [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]. Si es posible, suspender el análisis en toda la matriz [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)] árbol.

### <a name="licensing-agreements-for-unattended-installs"></a>Contratos de licencia para las instalaciones desatendidas

Si usa la línea de comandos para actualizar una instancia de SQL Server, asegúrese de que la línea de comandos incluye tanto el [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)] licencias parámetro de contrato y los nuevos parámetros de contrato de licencia de R y Python.

### <a name="offline-installation-of-machine-learning-components-for-a-localized-version-of-sql-server"></a>Instalación sin conexión de componentes de aprendizaje de máquina de una versión traducida de SQL Server

Cuando se instala [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)] componentes de aprendizaje de máquina en un equipo que no tiene acceso a internet, debe realizar algunos pasos adicionales:

+ Descargue a los instaladores de componentes de R o Python en una carpeta local antes de ejecutar el programa de instalación de SQL Server.
+ En algunos casos, deberá modificar el archivo de instalador para asegurarse de que está instalado el idioma correcto.
+ El identificador de idioma utilizado para los componentes de aprendizaje automático debe ser el mismo que el idioma del programa de instalación de SQL Server, o no se puede completar el programa de instalación.

Para obtener más información, consulte [instalación de componentes de aprendizaje de máquina sin acceso a internet](../r/installing-ml-components-without-internet-access.md).

## <a name="post-installation-configuration"></a>Configuración posterior a la instalación

Para usar el aprendizaje automático con R o Python, se requiere alguna configuración adicional después de ejecutar el programa de instalación de SQL Server. Los pasos precisos que se requieren dependen del nivel de seguridad del servidor y cómo se hayan configurado las bases de datos y la instancia de SQL Server.

Revise todas las opciones en la lista de instrucciones posteriores a la instalación para ver qué pasos adicionales pueden ser necesaria en su entorno.

+ [Configurar el equipo de SQL Server en la base de datos de aprendizaje](set-up-sql-server-r-services-in-database.md) 

## <a name="upgrades-or-uninstallation"></a>Las actualizaciones o la desinstalación

Esta sección contiene instrucciones detalladas para escenarios de actualización específicos.

### <a name="how-to-upgrade-sql-server"></a>Cómo actualizar SQL Server

Puede actualizar la versión de SQL Server volviendo a ejecutar el Asistente para la instalación.

+ [Actualizar SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)
+ [Actualizar SQL Server mediante el Asistente para la instalación](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

Puede actualizar solo la máquina de aprendizaje componentes mediante el uso de un proceso llamado enlace: 
+ [Usar SqlBindR para actualizar los componentes de aprendizaje de máquina](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

### <a name="end-of-support-for-in-place-upgrades-from-prerelease-versions"></a>Finalización del soporte para actualizaciones inmediatas de versiones preliminares

Ya no se admiten actualizaciones de versiones preliminares de SQL Server 2016. Esto incluye SQL Server 2016 CTP3, CTP3.1, CTP 3.2, RC0 o RC1.

Las siguientes versiones se instalaron con versiones preliminares de SQL Server 2016.

| Versión | Compilar         |
|---------|---------------|
| CTP 3.0 | 13.0.xxx      |
| CTP 3.1 | 13.0.801.12   |
| CTP 3.2 | 13.0.900.73   |
| CTP 3.3 | 13.0.1000.281 |
| RC1     | 13.0.1200.242 |
| RC2     | 13.0.1300.275 |
| RC3     | 13.0.1400.361 |

Si tiene alguna duda sobre a qué versión está utilizando, ejecute `@@VERSION` en una consulta de SQL Server Management Studio.

En general, el proceso de actualización es como sigue:

1. Realizar una copia de las secuencias de comandos y los datos.
2. Desinstale la versión preliminar.
3. Instale una versión de lanzamiento.

Desinstalar una versión preliminar de SQL Server componentes de aprendizaje de máquina pueden ser complejos y pudieron requerir la ejecución de un script especial. Póngase en contacto con el soporte técnico para obtener ayuda.

### <a name="support-for-slipstream-upgrades"></a>Compatibilidad con actualizaciones de instalación integrada

Por instalación integrada se entiende la capacidad de aplicar una revisión o actualización a una instalación de instancia con errores con el propósito de reparar problemas existentes. La ventaja de este método es que SQL Server se actualiza al mismo tiempo que realiza el programa de instalación, evitar un reinicio independiente más adelante.

Si el servidor no tiene acceso a internet, asegúrese de descargar al instalador de SQL Server. También debe descargar por separado las versiones que coinciden con los instaladores de componentes de R *antes de* comenzar el proceso de actualización. 

Para ubicaciones de descarga, vea [instalación de componentes de aprendizaje de máquina sin acceso a internet](installing-ml-components-without-internet-access.md).

Después de copiar todos los archivos de instalación en un directorio local, inicie la utilidad de instalación escribiendo SETUP.EXE en la línea de comandos.

- Use la */UpdateSource* argumento para especificar la ubicación de un archivo local que contiene la actualización de SQL Server, como una actualización acumulativa o la versión de service pack.

- Use la */MRCACHEDIRECTORY* argumento para especificar la carpeta que contiene los archivos CAB de componentes de R.

Para obtener más información, consulte este blog del equipo de soporte técnico: [implementar R Services en equipos sin acceso a internet](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/).

### <a name="get-machine-learning-components-for-offline-installs"></a>Obtener los componentes de aprendizaje de máquina para las instalaciones sin conexión

Si instalar o actualizar los servidores que no están conectados a internet, debe descargar una versión actualizada de la máquina de aprendizaje componentes manualmente antes de comenzar la actualización. 

+ [Instalación de componentes de aprendizaje de máquina sin acceso a internet](../../advanced-analytics/r/installing-ml-components-without-internet-access.md).

### <a name="support-policy-and-schedule-for-update-of-machine-learning-components"></a>Admite la directiva y la programación de actualización de componentes de aprendizaje de máquina

A medida que se publiquen las revisiones o mejoras en SQL Server, componentes de aprendizaje de máquina se actualiza automáticamente o se actualizan si la instancia ya incluye la característica.

A partir de 2016 de diciembre, puede actualizar los componentes de aprendizaje de máquina a un ritmo más rápido que el ciclo de versiones de SQL Server. Para ello, *enlace* una instancia de SQL Server a la directiva de ciclo de vida de Software modernas. Cada vez que se lanza una nueva versión de las herramientas de aprendizaje automático por el equipo de desarrollo de aprendizaje automático, puede descargar la versión más reciente y aplicarla a una instancia de SQL Server que se usa para el aprendizaje automático.

Para obtener más información, vea:

+ [Escala de tiempo del soporte técnico de Microsoft R Server y servidor de aprendizaje de máquina](https://docs.microsoft.com/machine-learning-server/resources-servicing-support)
+ [Usar SqlBindR para actualizar una instancia de SQL Server](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

## <a name="r-server-standalone"></a>R Server (Standalone)

Esta sección describen los problemas específicos de las instalaciones de Microsoft R Server (independiente) que use el programa de instalación de SQL Server 2016. 

Para problemas relacionados con las actualizaciones del servidor de R al servidor de aprendizaje de máquina, vea [instalar servidor para aprendizaje máquina con Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).

### <a name="problems-when-r-services-and-r-server-standalone-are-installed-on-the-same-computer"></a>Problemas cuando se instalan los servicios de R y R Server independiente en el mismo equipo

En versiones anteriores de SQL Server 2016, instalar R Server (independiente) y R Services (In-Database) al mismo tiempo a veces provocaba que el programa de instalación producirá un error con un mensaje de "acceso denegado". Este problema se corrigió en el Service Pack 1 para SQL Server 2016.

Si este error y que deba actualizar estas características, realizar una instalación integrada de SQL Server 2016 con SP1. Hay dos formas para resolver el problema, ambos de los cuales requieren desinstalar y volver a instalar.

1. Desinstale R Services (In-Database) y asegúrese de que se quitan las cuentas de usuario para SQLRUserGroup.

2. Reinicie el servidor y, a continuación, vuelva a instalar R Server (independiente).

3. Ejecutar SQL Server el programa de instalación una vez más, y esta vez seleccione **agregar características a SQL Server existente**.

4. Elija la instancia y, a continuación, seleccione la **R Services (In-Database)** opción para agregar.

Si este procedimiento no se puede resolver el problema, pruebe la siguiente solución alternativa:

1. Desinstale R Services (In-Database) y R Server (independiente) al mismo tiempo.

2. Quite las cuentas de usuario local (SQLRUserGroup).

3. Reinicie el servidor.

4. Ejecute el programa de instalación de SQL Server y agregar sólo la función de R Services (In-Database). No seleccione **R Server (independiente)**.

Por lo general, se recomienda no instalar R Services (In-Database) y R Server (independiente) en el mismo equipo. Sin embargo, suponiendo que el servidor tiene una capacidad suficiente, podría encontrar que r Server independiente puede resultar útil como herramienta de desarrollo. Otro escenario posible es que debe usar las características de puesta en marcha de R Server, pero también desea tener acceso a datos de SQL Server sin el movimiento de datos.

## <a name="see-also"></a>Vea también

 [Introducción a SQL Server R Services](../r/getting-started-with-sql-server-r-services.md)

 [Introducción a Microsoft R Server independiente](../r/getting-started-with-microsoft-r-server-standalone.md)
