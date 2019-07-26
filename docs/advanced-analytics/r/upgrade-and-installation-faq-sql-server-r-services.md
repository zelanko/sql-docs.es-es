---
title: Preguntas más frecuentes sobre la actualización y la instalación
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
ms.author: davidph
author: dphansen
ms.openlocfilehash: 0ee8902dad88cc148481585aaa9e1e083e536d0f
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469900"
---
# <a name="upgrade-and-installation-faq-for-sql-server-machine-learning-or-r-server"></a>Preguntas más frecuentes sobre actualización e instalación de SQL Server Machine Learning o R Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este tema se proporcionan respuestas a algunas preguntas comunes sobre la instalación de características de aprendizaje automático en SQL Server. También se tratan las preguntas más frecuentes sobre las actualizaciones.

+ Algunos problemas solo se producen con las actualizaciones de versiones preliminares. Por lo tanto, se recomienda identificar primero la versión y la edición antes de leer estas notas. Para obtener información de versión, `@@VERSION` ejecute en una consulta de SQL Server Management Studio.
+ Actualice a la versión más reciente o al lanzamiento de servicio tan pronto como sea posible para resolver cualquier problema corregido en las versiones recientes.

**Se aplica a:** SQL Server 2016 R Services, SQL Server 2017 Machine Learning Services (in-Database)

## <a name="requirements-and-restrictions-on-older-versions-of-sql-server-2016"></a>Requisitos y restricciones en versiones anteriores de SQL Server 2016 

En función de la compilación de SQL Server que esté instalando, podrían aplicarse algunas de las limitaciones siguientes:

- En las primeras versiones de SQL Server 2016 R Services, se necesitaba una notación 8.3 en la unidad que contiene el directorio de trabajo. Si ha instalado una versión preliminar, la actualización a SQL Server 2016 Service Pack 1 debe corregir este problema. Este requisito no se aplica a las versiones posteriores a SP1.

- Actualmente, no se puede [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] instalar en un clúster de conmutación por error. Sin embargo, SQL Server versión preliminar 2019 proporciona compatibilidad con la conmutación por error si desea evaluar esta funcionalidad en un entorno de prueba. Para obtener más información, [Consulte las](../what-s-new-in-sql-server-machine-learning-services.md)novedades.

- En una máquina virtual de Azure, es posible que se necesite una configuración adicional. Por ejemplo, puede que necesite crear una excepción de Firewall para admitir el acceso remoto.

- No se admite la instalación en paralelo con otra versión de R ni con otras versiones del análisis de revolución.

- Deshabilite el examen de virus antes de iniciar la instalación. Una vez completada la instalación, se recomienda suspender el análisis de virus en [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]las carpetas que usa. Preferiblemente, suspenda el examen en [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] todo el árbol.

 - Instalación de Microsoft R Server en una instancia de SQL Server instalada en Windows Core. En la versión RTM de SQL Server 2016, se produjo un problema conocido al agregar Microsoft R Server a una instancia en Windows Server Core Edition. Esto se ha solucionado. Si se produce este problema, puede aplicar la corrección descrita en [KB3164398](https://support.microsoft.com/kb/3164398) para agregar la característica de R a la instancia existente en Windows Server Core. Para obtener más información, consulte [No se puede instalar Microsoft R Server (independiente) en un sistema operativo Windows Server Core](https://support.microsoft.com/kb/3168691).


## <a name="offline-installation-of-machine-learning-components-for-a-localized-version-of-sql-server-2016"></a>Instalación sin conexión de componentes de machine learning para una versión localizada de SQL Server 2016

Las versiones preliminares de SQL Server 2016 no pudieron instalar los archivos. CAB específicos de la configuración regional durante la instalación sin conexión a Internet. Este problema se corrigió en versiones posteriores, pero si el instalador devuelve un mensaje que indica que no puede instalar el idioma correcto, puede editar el nombre de archivo para que el programa de instalación pueda continuar.

+ Edite manualmente el archivo del instalador para asegurarse de que está instalado el idioma correcto. Por ejemplo, para instalar la versión en japonés de SQL Server, cambiaría el nombre del archivo de SRS_ 8.0.3.0 _**1033**. cab a srs_ 8.0.3.0 _**1041**. cab.
+ El identificador de idioma que se usa para los componentes de aprendizaje automático debe ser el mismo que el idioma del programa de instalación de SQL Server, o bien no puede completar el programa de instalación.

## <a name="pre-release-versions-support-policies-upgrade-and-known-issues"></a>Versiones preliminares: directivas de soporte técnico, actualización y problemas conocidos

Ya no se admiten las nuevas instalaciones de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] versiones preliminares de. Si usa una versión preliminar, actualícelo lo antes posible.

Esta sección contiene instrucciones detalladas para escenarios de actualización específicos.

### <a name="how-to-upgrade-sql-server"></a>Cómo actualizar SQL Server

Puede actualizar la versión de SQL Server volviendo a ejecutar el Asistente para la instalación.

+ [Actualizar SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)
+ [Actualizar SQL Server con el Asistente para la instalación](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

Solo puede actualizar los componentes de machine learning mediante un proceso llamado enlace: 
+ [Uso de SqlBindR para actualizar componentes de aprendizaje automático](../install/upgrade-r-and-python.md)

### <a name="end-of-support-for-in-place-upgrades-from-prerelease-versions"></a>Fin de la compatibilidad con las actualizaciones en contexto de versiones preliminares

Ya no se admiten las actualizaciones de versiones preliminares de SQL Server 2016. Esto incluye SQL Server 2016 CTP3, CTP 3.1, CTP 3.2, RC0 o RC1.

Se instalaron las siguientes versiones con versiones preliminares de SQL Server 2016.

| `Version` | Compilación         |
|---------|---------------|
| CTP 3.0 | 13.0.xxx      |
| CTP 3.1 | 13.0.801.12   |
| CTP 3.2 | 13.0.900.73   |
| CTP 3.3 | 13.0.1000.281 |
| RC1     | 13.0.1200.242 |
| RC2     | 13.0.1300.275 |
| RC3     | 13.0.1400.361 |

Si tiene dudas sobre qué versión está usando, ejecute `@@VERSION` en una consulta de SQL Server Management Studio.

En general, el proceso de actualización es el siguiente:

1. Realizar copias de seguridad de scripts y datos.
2. Desinstale la versión preliminar.
3. Instale una versión de lanzamiento.

La desinstalación de una versión preliminar del SQL Server componentes de machine learning puede ser compleja y requerir la ejecución de un script especial. Póngase en contacto con el soporte técnico para obtener ayuda.

###  <a name="bkmk_Uninstall"></a>Desinstalar antes de actualizar desde una versión anterior de Microsoft R Server

Si ha instalado una versión preliminar de Microsoft R Server, debe desinstalarla para poder actualizar a una versión más reciente.

1.  En el **Panel de control**, haga clic en **Agregar o quitar programas**y seleccione `Microsoft SQL Server 2016 <version number>`.

2.  En el cuadro de diálogo con opciones para **Agregar**, **Reparar**o **Quitar** componentes, seleccione **Quitar**.
  
3.  En la página **Seleccionar características** , en **Características compartidas**, seleccione **R Server (independiente)** . Haga clic en **Siguiente**y, después, haga clic en **Finalizar** para desinstalar los componentes seleccionados.

## <a name="r-services-and-r-server-standalone-side-by-side-errors"></a>R Services y R Server (independiente) errores en paralelo 

En versiones anteriores de SQL Server 2016, la instalación de R Server (independiente) y R Services (en base de datos) al mismo tiempo ocasionaba que el programa de instalación produjera un error con el mensaje "acceso denegado". Este problema se corrigió en el Service Pack 1 para SQL Server 2016.

Si se produjo este error y necesita actualizar estas características, realice una instalación integrada de SQL Server 2016 con SP1. Hay dos maneras de resolver el problema, que requieren la desinstalación y reinstalación de.

1. Desinstale R Services (en base de datos) y asegúrese de que las cuentas de usuario de SQLRUserGroup se han quitado.

2. Reinicie el servidor y vuelva a instalar R Server (independiente).

3. Ejecute SQL Server instalación una vez más y, esta vez, seleccione **Agregar características a SQL Server existentes**.

4. Elija la instancia y, a continuación, seleccione la opción **R Services (en base de datos)** para agregar.

Si este procedimiento no soluciona el problema, pruebe la siguiente solución alternativa:

1. Desinstale R Services (en base de datos) y R Server (independiente) al mismo tiempo.

2. Quite las cuentas de usuario locales (SQLRUserGroup).

3. Reinicie el servidor.

4. Ejecute el programa de instalación de SQL Server y agregue la característica R Services (solo en la base de datos). No seleccione **R Server (independiente)** .

Por lo general, se recomienda no instalar R Services (en bases de datos) y R Server (independiente) en el mismo equipo. Sin embargo, suponiendo que el servidor tiene una capacidad suficiente, podría encontrar R Server independiente podría ser útil como herramienta de desarrollo. Otro escenario posible es que necesite usar las características de operacionalización de R Server, pero también quiere acceder a los datos de SQL Server sin movimiento de datos.

## <a name="incompatible-version-of-r-client-and-r-server"></a>Versión incompatible del Cliente de R y R Server

Si instala Microsoft R Client y lo usa para ejecutar R en un contexto de cálculo de SQL Server remoto, podría obtener un error similar al siguiente:

*Está ejecutando la versión 9.0.0 del cliente de Microsoft R en el equipo, que es incompatible con la versión de Microsoft R Server 8.0.3. Download and install a compatible version.* (Está ejecutando la versión 9.0.0 del Cliente de Microsoft R en el equipo, que es incompatible con Microsoft R Server versión 8.0.3. Descargue e instale una versión compatible).

En SQL Server 2016, era necesario que la versión de R que se ejecutaba en SQL Server R Services sea exactamente la misma que las bibliotecas de Microsoft R Client. Ese requisito se ha quitado en versiones posteriores. Sin embargo, se recomienda obtener siempre las versiones más recientes de los componentes de aprendizaje automático e instalar todos los Service Packs. 

Si tiene una versión anterior de Microsoft R Server y necesita garantizar la compatibilidad con Microsoft R Client 9.0.0, instale las actualizaciones que se describen en este [artículo de soporte técnico](https://support.microsoft.com/kb/3210262).


## <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>La instalación no puede llevarse a cabo y se genera el siguiente error: "Only one Revolution Enterprise product can be installed at a time." (Solo se puede instalar de cada vez un producto Revolution Enterprise).

Es posible que se produzca este error si tiene una instalación anterior de productos Revolution Analytics o una versión preliminar de SQL Server R Services. Debe desinstalar todas las versiones anteriores para poder instalar una versión más reciente de Microsoft R Server. No se admite la instalación en paralelo con otras versiones de herramientas de Revolution Enterprise.

En cambio, se admiten las instalaciones en paralelo cuando se usa R Server (independiente) con [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] o SQL Server 2016.

## <a name="registry-cleanup-to-uninstall-older-components"></a>Limpieza del registro para desinstalar componentes anteriores

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

 [SQL Server Machine Learning Services (in-Database)](../r/sql-server-r-services.md)

 [SQL Server Machine Learning Server (independiente)](../r/r-server-standalone.md)
