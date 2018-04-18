---
title: Preguntas más frecuentes de actualización e instalación para el aprendizaje automático de SQL Server | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 52ff43f13ff3f17f21ed96313d3134d8ee31dd86
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="upgrade-and-installation-faq-for-sql-server-machine-learning-or-r-server"></a>P+f sobre la actualización e instalación de aprendizaje automático de SQL Server o servidor de R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este tema proporciona respuestas a algunas preguntas comunes acerca de la instalación de características de SQL Server de aprendizaje automático. Además se ocupa de las preguntas habituales acerca de las actualizaciones.

+ Se producen algunos problemas sólo con las actualizaciones de versiones preliminares. Por lo tanto, se recomienda que identificar la versión y edición primero antes de leer estas notas. Para obtener información de versión, ejecute `@@VERSION` en una consulta de SQL Server Management Studio.
+ Actualice a la versión más reciente o la versión de servicio tan pronto como sea posible, para resolver los problemas que se corrigieron en las versiones recientes.

**Se aplica a:** (en bases de datos) de servicios de aprendizaje de automático de SQL Server 2016 R Services, SQL Server de 2017

## <a name="requirements-and-restrictions-on-older-versions-of-sql-server-2016"></a>Requisitos y restricciones de las versiones anteriores de SQL Server 2016 

Dependiendo de la compilación de SQL Server que va a instalar, se podrían aplicar algunas de las siguientes limitaciones:

- En las versiones anteriores de SQL Server 2016 R Services, se requería la notación de tiene el formato 8.3 en la unidad que contiene el directorio de trabajo. Si instaló una versión preliminar, la actualización a Service Pack 1 de SQL Server 2016 debe solucionar este problema. Este requisito no se aplica a las versiones después del SP1.

- Instalación de en paralelo con otra versión de R, o con otras versiones de Revolution Analytics, no se admite.

- Deshabilitar el antivirus antes de comenzar el programa de instalación. Una vez completada la instalación, se recomienda suspender la detección de virus en las carpetas usadas por [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]. Si es posible, suspender el análisis en toda la matriz [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)] árbol.

 - Instalar Microsoft R Server en una instancia de SQL Server instalada en el núcleo de Windows. En la versión RTM de SQL Server 2016, se produjo un problema conocido al agregar Microsoft R Server en una instancia de la edición de Windows Server Core. Esto se ha solucionado. Si se produce este problema, puede aplicar la revisión que se describe en [KB3164398](https://support.microsoft.com/kb/3164398) para agregar la característica de R a la instancia existente en Windows Server Core. Para obtener más información, consulte [No se puede instalar Microsoft R Server (independiente) en un sistema operativo Windows Server Core](https://support.microsoft.com/kb/3168691).


## <a name="offline-installation-of-machine-learning-components-for-a-localized-version-of-sql-server-2016"></a>Instalación sin conexión de componentes de aprendizaje de máquina de una versión traducida de SQL Server 2016

Primeras versiones de SQL Server 2016 no se pudo instalar archivos .cab de configuración regional durante la instalación sin conexión sin una conexión a internet. Este problema se ha corregido en versiones posteriores, pero si el programa de instalación devuelve un mensaje que indica que no puede instalar el idioma correcto, puede editar el nombre de archivo para permitir que continúe la instalación.

+ Editar manualmente el archivo de instalador para asegurarse de que está instalado el idioma correcto. Por ejemplo, para instalar la versión en japonés de SQL Server, cambiaría el nombre del archivo de SRS_8.0.3.0_**1033**.cab a SRS_8.0.3.0_**1041**.cab.
+ El identificador de idioma utilizado para los componentes de aprendizaje automático debe ser el mismo que el idioma del programa de instalación de SQL Server, o no se puede completar el programa de instalación.

## <a name="pre-release-versions-support-policies-upgrade-and-known-issues"></a>Versiones preliminares: compatible con las directivas, actualización y problemas conocidos

Las nuevas instalaciones de cualquier versión preliminar de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] ya no se admite. Si está utilizando una versión preliminar, actualizar tan pronto como sea posible.

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

###  <a name="bkmk_Uninstall"></a> Desinstale antes de actualizar desde una versión anterior de Microsoft R Server

Si ha instalado una versión preliminar de Microsoft R Server, debe desinstalarla para poder actualizar a una versión más reciente.

1.  En el **Panel de control**, haga clic en **Agregar o quitar programas**y seleccione `Microsoft SQL Server 2016 <version number>`.

2.  En el cuadro de diálogo con opciones para **Agregar**, **Reparar**o **Quitar** componentes, seleccione **Quitar**.
  
3.  En la página **Seleccionar características** , en **Características compartidas**, seleccione **R Server (independiente)**. Haga clic en **Siguiente**y, después, haga clic en **Finalizar** para desinstalar los componentes seleccionados.

## <a name="r-services-and-r-server-standalone-side-by-side-errors"></a>R Services y errores de side-by-side R Server (independiente) 

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

## <a name="incompatible-version-of-r-client-and-r-server"></a>Versión incompatible del Cliente de R y R Server

Si instala al cliente de Microsoft R y utilizarlo para ejecutar R en un contexto de proceso de SQL Server remoto, podría obtener un error similar al siguiente:

*Está ejecutando la versión 9.0.0 del cliente de Microsoft R en el equipo, que es incompatible con la versión 8.0.3 de Microsoft R Server. Download and install a compatible version.* (Está ejecutando la versión 9.0.0 del Cliente de Microsoft R en el equipo, que es incompatible con Microsoft R Server versión 8.0.3. Descargue e instale una versión compatible).

En SQL Server 2016, era necesario que la versión de R que se estaba ejecutando en SQL Server R Services ser exactamente igual que las bibliotecas de cliente de Microsoft R. Ese requisito se ha quitado en versiones posteriores. Sin embargo, se recomienda que siempre obtener las últimas versiones de los componentes de aprendizaje automático e instale todos los service packs. 

Si tiene una versión anterior de Microsoft R Server y necesita garantizar su compatibilidad con el cliente de Microsoft R 9.0.0, instale las actualizaciones que se describen en este [artículo de soporte técnico](https://support.microsoft.com/kb/3210262).


## <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>La instalación no puede llevarse a cabo y se genera el siguiente error: "Only one Revolution Enterprise product can be installed at a time." (Solo se puede instalar de cada vez un producto Revolution Enterprise).

Es posible que se produzca este error si tiene una instalación anterior de productos Revolution Analytics o una versión preliminar de SQL Server R Services. Debe desinstalar todas las versiones anteriores para poder instalar una versión más reciente de Microsoft R Server. No se admite la instalación en paralelo con otras versiones de herramientas de Revolution Enterprise.

En cambio, se admiten las instalaciones en paralelo cuando se usa R Server (independiente) con [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] o SQL Server 2016.

## <a name="registry-cleanup-to-uninstall-older-components"></a>Limpieza del registro para desinstalar los componentes anteriores

Si tiene problemas para quitar una versión anterior, puede que deba editar el Registro para quitar las claves relacionadas.

> [!IMPORTANT]
> Este problema se produce únicamente si ha instalado una versión preliminar de Microsoft R Server o una versión CTP de SQL Server 2016 R Services.
  
1. Abra el Registro de Windows y busque esta clave: `HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`.
2. Elimine todas las entradas siguientes, si están presentes, y si la clave solo contiene el valor `sEstimatedSize2`:
  
    -   E0B2C29E-B8FC-490B-A043-2CAE75634972        (para 8.0.2)
  
    -   46695879-954E-4072-9D32-1CC84D4158F4        (para 8.0.1)
  
    -   2DF16DF8-A2DB-4EC6-808B-CB5A302DA91B        (para 8.0.0)
  
    -   5A2A1571-B8CD-4AAF-9303-8DF463DABE5A        (para 7.5.0)

## <a name="see-also"></a>Vea también

 [Equipo con SQL Server (en bases de datos) de servicios de aprendizaje](../r/sql-server-r-services.md)

 [Máquina del servidor SQL Server (independiente) de aprendizaje](../r/r-server-standalone.md)
