---
title: Preguntas más frecuentes sobre actualización e instalación
description: Respuestas a algunas preguntas comunes sobre la instalación de características de aprendizaje automático en SQL Server.
ms.custom: seo-lt-2019
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/06/2019
ms.topic: conceptual
ms.author: davidph
author: dphansen
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6357f98627842ab790b494cf1b4a1f9b2110ec9c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "73727349"
---
# <a name="upgrade-and-installation-faq-for-sql-server-machine-learning-or-r-server"></a>Preguntas más frecuentes sobre actualización e instalación de SQL Server Machine Learning o R Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este tema se ofrecen respuestas a algunas preguntas comunes sobre la instalación de características de aprendizaje automático en SQL Server. También se tratan algunas preguntas habituales sobre actualizaciones.

+ Algunos problemas solo se producen con las actualizaciones de versiones preliminares. Por lo tanto, se recomienda identificar primero la versión y la edición antes de leer estas notas. Para obtener la información de versión, ejecute `@@VERSION` en una consulta de SQL Server Management Studio.
+ Actualice a la versión más reciente o la versión de servicio en cuanto pueda para resolver cualquier problema corregido en las versiones recientes.

**Se aplica a:** SQL Server 2016 R Services, SQL Server Machine Learning Services (en la base de datos)

## <a name="requirements-and-restrictions-on-older-versions-of-sql-server-2016"></a>Requisitos y restricciones en versiones anteriores de SQL Server 2016 

En función de la compilación de SQL Server que vaya a instalar, podrían aplicarse algunas de las limitaciones siguientes:

- En las primeras versiones de SQL Server 2016 R Services, se necesitaba una notación 8dot3 en la unidad que contiene el directorio de trabajo. Si tenía instalada una versión preliminar, el problema se corregía al actualizar a SQL Server 2016 Service Pack 1. Este requisito no se aplica a las versiones posteriores a SP1.

- No se puede instalar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] en un clúster de conmutación por error en SQL Server 2016. Sin embargo, SQL Server 2019 sí admite la conmutación por error. Para más información, vea [Novedades](../what-s-new-in-sql-server-machine-learning-services.md).

- En una máquina virtual de Azure, es posible que se necesite una configuración adicional. Por ejemplo, puede que necesite crear una excepción de firewall para admitir el acceso remoto.

- No se admite la instalación en paralelo con otra versión de R ni con otras versiones de Revolution Analytics.

- Deshabilite el análisis antivirus antes de iniciar la instalación. Una vez completada la instalación, se recomienda suspender el análisis antivirus en las carpetas usadas por [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]. Es preferible que suspenda el análisis en todo el árbol de [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)].

 - Instalar Microsoft R Server en una instancia de SQL Server instalada en Windows Core. En la versión de RTM de SQL Server 2016, se producía un problema conocido al agregar Microsoft R Server a una instancia de Windows Server Core Edition. Esto se ha solucionado. Si se produce este problema, puede aplicar la revisión que se describe en [KB3164398](https://support.microsoft.com/kb/3164398) para agregar la característica R a la instancia existente en Windows Server Core. Para obtener más información, consulte [No se puede instalar Microsoft R Server (independiente) en un sistema operativo Windows Server Core](https://support.microsoft.com/kb/3168691).


## <a name="offline-installation-of-machine-learning-components-for-a-localized-version-of-sql-server-2016"></a>Instalación sin conexión de componentes de aprendizaje automático para una versión localizada de SQL Server 2016

Las versiones preliminares de SQL Server 2016 no podían instalar archivos .cab específicos de la configuración regional durante la instalación sin una conexión a Internet. Este problema se corrigió en versiones posteriores, pero si el instalador muestra un mensaje que indica que no puede instalar el idioma correcto, puede editar el nombre de archivo para poder continuar con la instalación.

+ Edite manualmente el archivo del instalador para asegurarse de que está instalado el idioma correcto. Por ejemplo, para instalar la versión en japonés de SQL Server, deberá cambiar el nombre del archivo de SRS_8.0.3.0_**1033**.cab a SRS_8.0.3.0_**1041**.cab.
+ El identificador de idioma que se usa para los componentes de aprendizaje automático debe ser el mismo que el idioma del programa de instalación de SQL Server; de no ser así, no podrá completar el programa de instalación.

## <a name="pre-release-versions-support-policies-upgrade-and-known-issues"></a>Versiones preliminares: políticas de soporte técnico, actualización y problemas conocidos

Ya no se admite la instalación nueva de versiones preliminares de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Si está usando una versión preliminar, actualícela lo antes posible.

Esta sección contiene instrucciones detalladas para escenarios de actualización específicos.

### <a name="how-to-upgrade-sql-server"></a>Procedimiento para actualizar SQL Server

Para actualizar la versión de SQL Server, solo tiene que volver a ejecutar el asistente para la instalación.

+ [Actualizar SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)
+ [Actualización de SQL Server con el asistente para instalación](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

Puede actualizar solo los componentes de aprendizaje automático si usa un proceso llamado enlace: 
+ [Uso de SqlBindR para actualizar componentes de aprendizaje automático](../install/upgrade-r-and-python.md)

### <a name="end-of-support-for-in-place-upgrades-from-prerelease-versions"></a>Fin de la compatibilidad para actualizaciones en contexto de versiones preliminares

Ya no se admite la actualización de versiones preliminares de SQL Server 2016. Esto incluye SQL Server 2016 CTP3, CTP3.1, CTP3.2, RC0 o RC1.

Estas versiones se instalaron con versiones preliminares de SQL Server 2016.

| Versión | Build         |
|---------|---------------|
| CTP 3.0 | 13.0.xxx      |
| CTP 3.1 | 13.0.801.12   |
| CTP 3.2 | 13.0.900.73   |
| CTP 3.3 | 13.0.1000.281 |
| RC1     | 13.0.1200.242 |
| RC2     | 13.0.1300.275 |
| RC3     | 13.0.1400.361 |

Si tiene dudas sobre qué versión está usando, ejecute `@@VERSION` en una consulta desde SQL Server Management Studio.

En general, este es el proceso de actualización:

1. Realizar copia de seguridad de scripts y datos.
2. Desinstalar la versión preliminar.
3. Instalar una versión de lanzamiento.

La desinstalación de una versión preliminar de los componentes de aprendizaje automático de SQL Server puede ser compleja y podría ser necesario ejecutar un script especial. Póngase en contacto con el soporte técnico para obtener ayuda.

###  <a name="bkmk_Uninstall"></a> Desinstalación antes de actualizar desde una versión anterior de Microsoft R Server

Si ha instalado una versión preliminar de Microsoft R Server, debe desinstalarla para poder actualizar a una versión más reciente.

1.  En el **Panel de control**, haga clic en **Agregar o quitar programas**y seleccione `Microsoft SQL Server 2016 <version number>`.

2.  En el cuadro de diálogo con opciones para **Agregar**, **Reparar**o **Quitar** componentes, seleccione **Quitar**.
  
3.  En la página **Seleccionar características** , en **Características compartidas**, seleccione **R Server (independiente)** . Haga clic en **Siguiente**y, después, haga clic en **Finalizar** para desinstalar los componentes seleccionados.

## <a name="r-services-and-r-server-standalone-side-by-side-errors"></a>Errores de R Services y R Server (independiente) en paralelo 

En versiones anteriores de SQL Server 2016, si se instalaba R Server (independiente) y R Services (en la base de datos) al mismo tiempo ocasionaba que el programa de instalación produjera un error con el mensaje "acceso denegado". Este problema se corrigió en el Service Pack 1 para SQL Server 2016.

Si obtuvo este error y necesita actualizar estas características, realice una instalación integrada de SQL Server 2016 con SP1. Hay dos maneras de resolver el problema, para las que tendrá que desinstalar y reinstalar.

1. Desinstale R Services (en la base de datos) y asegúrese de que las cuentas de usuario de SQLRUserGroup se han quitado.

2. Reinicie el servidor y reinstale R Server (independiente).

3. Vuelva a ejecutar la instalación de SQL Server y, esta vez, seleccione **Agregar características a SQL Server existente**.

4. Elija la instancia y seleccione la opción **R Services (en la base de datos)** que se va a agregar.

Si no se soluciona el problema, pruebe esta solución alternativa:

1. Desinstale R Services (en la base de datos) y R Server (independiente) al mismo tiempo.

2. Quite las cuentas de usuario locales (SQLRUserGroup).

3. Reinicie el servidor.

4. Ejecute el programa de instalación de SQL Server y agregue solamente la característica R Services (en la base de datos). No seleccione **R Server (independiente)** .

Por lo general, se recomienda no instalar R Services (en la base de datos) y R Server (independiente) en el mismo equipo. Pero si el servidor tiene suficiente capacidad, puede que R Server independiente le sea útil como herramienta de desarrollo. Otro escenario posible es que necesite usar las características de operacionalización de R Server, pero también quiera acceder a los datos de SQL Server sin movimiento de datos.

## <a name="incompatible-version-of-r-client-and-r-server"></a>Versión incompatible del Cliente de R y R Server

Si instala Microsoft R Client y lo usa para ejecutar R en un contexto de proceso de SQL Server remoto, podría obtener un error similar a este:

*You are running version 9.0.0 of Microsoft R client on your computer, which is incompatible with the Microsoft R Server version 8.0.3. Download and install a compatible version.* (Está ejecutando la versión 9.0.0 del Cliente de Microsoft R en el equipo, que es incompatible con Microsoft R Server versión 8.0.3. Descargue e instale una versión compatible).

En SQL Server 2016, era necesario que la versión de R que se ejecutaba en SQL Server R Services fuera exactamente la misma que la de las bibliotecas de Microsoft R Client. Este requisito se ha quitado en versiones posteriores. Aún así, se recomienda obtener siempre las versiones más recientes de los componentes de aprendizaje automático e instalar todos los Service Packs. 

Si tiene una versión anterior de Microsoft R Server y necesita garantizar la compatibilidad con Microsoft R Client 9.0.0, instale las actualizaciones que se describen en este [artículo de soporte técnico](https://support.microsoft.com/kb/3210262).


## <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>La instalación no puede llevarse a cabo y se genera el siguiente error: "Only one Revolution Enterprise product can be installed at a time." (Solo se puede instalar de cada vez un producto Revolution Enterprise).

Es posible que se produzca este error si tiene una instalación anterior de productos Revolution Analytics o una versión preliminar de SQL Server R Services. Debe desinstalar todas las versiones anteriores para poder instalar una versión más reciente de Microsoft R Server. No se admite la instalación en paralelo con otras versiones de herramientas de Revolution Enterprise.

En cambio, se admiten las instalaciones en paralelo cuando se usa R Server (independiente) con [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] o SQL Server 2016.

## <a name="registry-cleanup-to-uninstall-older-components"></a>Limpieza del Registro para desinstalar componentes anteriores

Si tiene problemas para quitar una versión anterior, puede que deba editar el Registro para quitar las claves relacionadas.

> [!IMPORTANT]
> Este problema se produce únicamente si ha instalado una versión preliminar de Microsoft R Server o una versión CTP de SQL Server 2016 R Services.
  
1. Abra el Registro de Windows y busque esta clave: `HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`.
2. Elimine todas las entradas siguientes, si están presentes, y si la clave solo contiene el valor `sEstimatedSize2`:
  
    -   E0B2C29E-B8FC-490B-A043-2CAE75634972        (para 8.0.2)
  
    -   46695879-954E-4072-9D32-1CC84D4158F4        (para 8.0.1)
  
    -   2DF16DF8-A2DB-4EC6-808B-CB5A302DA91B        (para 8.0.0)
  
    -   5A2A1571-B8CD-4AAF-9303-8DF463DABE5A        (para 7.5.0)

## <a name="see-also"></a>Consulte también

 [SQL Server Machine Learning Services (en la base de datos)](../r/sql-server-r-services.md)

 [SQL Server Machine Learning Server (independiente)](../r/r-server-standalone.md)
