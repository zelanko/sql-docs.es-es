---
title: Instalación sin acceso a Internet
description: Instalación de SQL Server Machine Learning (R y Python) en equipos aislados detrás de un firewall de red.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/04/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e966406a20df723c453a5c8083f00f2e4989d9d0
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "74064126"
---
# <a name="install-sql-server-machine-learning-r-and-python-on-computers-with-no-internet-access"></a>Instalación de SQL Server Machine Learning (R y Python) en equipos sin acceso a Internet
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

De forma predeterminada, los instaladores se conectan a sitios de descarga de Microsoft para obtener los componentes necesarios y actualizados de Machine Learning en SQL Server. Si las restricciones del firewall impiden que el instalador acceda a estos sitios, puede usar un dispositivo conectado a Internet para descargar archivos, transferirlos a un servidor sin conexión y, a continuación, ejecutar el programa de instalación.

El análisis en la base de datos consta de una instancia de motor de base de datos, además de componentes adicionales para la integración de R y Python, en función de la versión de SQL Server. 

+ SQL Server 2019 incluye R, Python y Java
+ SQL Server 2017 incluye R y Python
+ SQL Server 2016 es solo R

En un servidor aislado, las características específicas del idioma de Machine Learning y de R/Python se agregan mediante archivos CAB. 

::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
## <a name="sql-server-2019-offline-install"></a>Instalación sin conexión de SQL Server 2019

Para instalar SQL Server Machine Learning Services (R y Python) en un servidor aislado, empiece por descargar la versión inicial de SQL Server y los archivos CAB correspondientes para la compatibilidad con R y Python. Incluso si planea actualizar inmediatamente el servidor para que use la actualización acumulativa más reciente, primero se debe instalar una versión inicial.

> [!Note]
> SQL Server 2019 no tiene Service Packs. La versión inicial es la única línea base, con mantenimiento solo a través de actualizaciones acumulativas.

### <a name="1---download-2019-cabs"></a>1 - Descargar archivos CAB 2019

En un equipo que tenga conexión a Internet, descargue los archivos CAB que proporcionan características de R y Python para la versión inicial y los medios de instalación de SQL Server 2019.

Release  |Vínculo de descarga  |
---------|---------------|
Microsoft R Open        | [SRO_3.5.2.125_1033.cab](https://go.microsoft.com/fwlink/?linkid=2085686) |
Microsoft R Server      | [SRS_9.4.7.25_1033.cab](https://go.microsoft.com/fwlink/?linkid=2085792) |
Microsoft Python Open   | [SPO_4.5.12.120_1033.cab](https://go.microsoft.com/fwlink/?linkid=2085793) |
Microsoft Python Server | [SPS_9.4.7.25_1033.cab](https://go.microsoft.com/fwlink/?linkid=2085685) |

> [!NOTE]
> La característica de Java se incluye con los medios de instalación de SQL Server y no necesita un archivo CAB independiente.

###  <a name="2---get-sql-server-2019-installation-media"></a>2 - Obtener medios de instalación de SQL Server 2019

1. En un equipo que tenga conexión a Internet, descargue el [programa de instalación de SQL Server 2019](https://www.microsoft.com/sql-server/sql-server-downloads). 

2. Haga doble clic en la configuración y elija el tipo de instalación **Descargar medios**. Con esta opción, el programa de instalación crea un archivo local .iso (o .cab) que contiene el medio de instalación.

   ![Seleccione el tipo de instalación Descargar medios](media/2019offline-download-tile.png "Descargar medios")

::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
## <a name="sql-server-2017-offline-install"></a>Instalación sin conexión de SQL Server 2017

Para instalar SQL Server Machine Learning Services (R y Python) en un servidor aislado, empiece por descargar la versión inicial de SQL Server y los archivos CAB correspondientes para la compatibilidad con R y Python. Incluso si planea actualizar inmediatamente el servidor para que use la actualización acumulativa más reciente, primero se debe instalar una versión inicial.

> [!Note]
> SQL Server 2017 no tiene Service Packs. Es la primera versión de SQL Server que usa la versión inicial como única línea base, con mantenimiento solo a través de las actualizaciones acumulativas. 

### <a name="1---download-2017-cabs"></a>1 - Descargar archivos CAB 2017

En un equipo que tenga conexión a Internet, descargue los archivos CAB que proporcionan características de R y Python para la versión inicial y los medios de instalación de SQL Server 2017. 

Release  |Vínculo de descarga  |
---------|---------------|
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Microsoft Python Server    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |

###  <a name="2---get-sql-server-2017-installation-media"></a>2 - Obtener medios de instalación de SQL Server 2017

1. En un equipo que tenga conexión a Internet, descargue el [programa de instalación de SQL Server 2017](https://www.microsoft.com/sql-server/sql-server-downloads). 

2. Haga doble clic en la configuración y elija el tipo de instalación **Descargar medios**. Con esta opción, el programa de instalación crea un archivo local .iso (o .cab) que contiene el medio de instalación.

   ![Seleccione el tipo de instalación Descargar medios](media/offline-download-tile.png "Descargar medios")

::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

## <a name="sql-server-2016-offline-install"></a>Instalación sin conexión de SQL Server 2016

El análisis en base de datos de SQL Server 2016 es de solo R, con solo dos archivos CAB para los paquetes de productos y la distribución de Microsoft de R de código abierto, respectivamente. Empiece instalando cualquiera de estas versiones: RTM, SP 1, SP 2. Una vez efectuada una instalación base, las actualizaciones acumulativas se pueden aplicar como paso siguiente.

En un equipo que tenga conexión a Internet, descargue los archivos CAB usados por el programa de instalación para instalar el análisis de base de datos en SQL Server 2016. 

### <a name="1---download-2016-cabs"></a>1 - Descargar archivos CAB 2016

Release  | Microsoft R Open | Microsoft R Server |
---------|-----------------|---------------------|
**SQL Server 2016 RTM**     | [SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266) |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051) |
**SQL Server 2016 SP 1**     | [SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879) |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881) | 
**SQL Server 2016 SP 2**  |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866039) |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317) |

### <a name="2---get-sql-server-2016-installation-media"></a>2 - Obtener medios de instalación de SQL Server 2016

Puede instalar SQL Server 2016 RTM, SP 1 o SP 2 como primera instalación en el equipo de destino. Cualquiera de estas versiones puede aceptar una actualización acumulativa.

Un modo de obtener un archivo .iso que contiene el medio de instalación es con [Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/). Inicie sesión y, a continuación, use el vínculo **Descargas** para buscar la versión de SQL Server 2016 que quiere instalar. La descarga es un archivo .iso, que puede copiar en el equipo de destino para efectuar una instalación sin conexión.

::: moniker-end

## <a name="transfer-files"></a>Transferencia de archivos

Copie el medio de instalación de SQL Server (.iso o .cab) y los archivos CAB de análisis de base de datos en el equipo de destino. Coloque los archivos CAB y el archivo del medio de instalación en la misma carpeta del equipo de destino (por ejemplo, en la carpeta %TEMP% del usuario que realiza la instalación).

La carpeta %TEMP% es necesaria para los archivos CAB de Python. En cuanto a R, puede usar %TEMP% o establecer el parámetro `myrcachedirectory` en la ruta de acceso del archivo CAB.

## <a name="run-setup"></a>Ejecución del programa de instalación

Al ejecutar el programa de instalación de SQL Server en un equipo sin conexión a Internet, agrega una página de **instalación sin conexión** al asistente para que pueda especificar la ubicación de los archivos CAB que ha copiado en el paso anterior.

1. Para comenzar la instalación, haga doble clic en el archivo .iso o .cab para obtener acceso a los medios de instalación. Debería ver el archivo **setup. exe**.

2. Haga clic con el botón secundario en **setup.exe** y ejecútelo como administrador.

3. Cuando el asistente para la instalación muestre la página de licencias de los componentes de R o Python de código abierto, haga clic en **Aceptar**. La aceptación de los términos de licencia le permite continuar con el siguiente paso.

4. Cuando llegue a la página **Instalación sin conexión**, en **Ruta de instalación**, especifique la carpeta que contiene los archivos CAB que ha copiado antes.

5. Siga las indicaciones en pantalla para completar la instalación.

<a name="apply-cu"></a>

## <a name="apply-cumulative-updates"></a>Aplicación de actualizaciones acumulativas

Se recomienda aplicar la última actualización acumulativa tanto en el motor de base de datos como en los componentes de Machine Learning. Las actualizaciones acumulativas se instalan a través del programa de instalación. 

::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
1. Comience con una instancia de línea base. Solo puede aplicar las actualizaciones acumulativas a las instalaciones existentes de la versión inicial de SQL Server.

2. En un dispositivo conectado a Internet, vaya a la lista de actualizaciones acumulativas correspondientes a su versión de SQL Server:

   + Actualizaciones de SQL Server 2019 *(las actualizaciones aún no están disponibles para la versión 2019)*
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
1. Comience con una instancia de línea base. Solo puede aplicar las actualizaciones acumulativas a las instalaciones existentes de la versión inicial de SQL Server.

2. En un dispositivo conectado a Internet, vaya a la lista de actualizaciones acumulativas correspondientes a su versión de SQL Server:

   + [Actualizaciones de SQL Server 2017](https://sqlserverupdates.com/sql-server-2017-updates/)
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
1. Comience con una instancia de línea base. Solo puede aplicar actualizaciones acumulativas a las instalaciones existentes de la versión inicial de SQL Server 2016, SQL Server 2016 SP 1 o SQL Server 2016 SP 2.

2. En un dispositivo conectado a Internet, vaya a la lista de actualizaciones acumulativas correspondientes a su versión de SQL Server:

   + [Actualizaciones de SQL Server 2016](https://sqlserverupdates.com/sql-server-2016-updates/)
::: moniker-end

3. Seleccione la actualización acumulativa más reciente para descargar el archivo ejecutable.

4. Obtenga los archivos .CAB correspondientes a R y Python. Para obtener los vínculos de descarga, vea [Descargas de CAB de actualizaciones acumulativas en instancias de análisis en base de datos de SQL Server](sql-ml-cab-downloads.md).

5. Transfiera todos los archivos, archivos ejecutables y archivos CAB a la misma carpeta del equipo sin conexión.

6. Ejecute el programa de instalación. Acepte los términos de licencia y, en la página de selección de características, revise las características para las que se aplican las actualizaciones acumulativas. Debería ver todas las características instaladas para la instancia actual, incluidas las características de aprendizaje automático.

   ![Selección de características en el árbol de características](media/cumulative-update-feature-selection.png "Lista de características")

5. Continúe con los pasos del asistente y acepte los términos de licencia para las distribuciones de R y Python. Durante la instalación se le pedirá que elija la ubicación de la carpeta que contiene los archivos CAB actualizados.

## <a name="set-environment-variables"></a>Establecimiento de variables de entorno

Solo de cara a la integración de características de R, conviene establecer la variable de entorno **MKL_CBWR** para [garantizar una salida coherente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) de los cálculos de la biblioteca Math Kernel Library (MKL) de Intel.

1. En el panel de control, haga clic en **Sistema y seguridad** > **Sistema** > **Configuración avanzada del sistema** > **Variables de entorno**.

2. Cree un usuario o una variable del sistema. 

   + Establezca el nombre de la variable en `MKL_CBWR`.
   + Establezca el valor de la variable en `AUTO`.

Este paso requiere el reinicio del servidor. Si va a habilitar la ejecución de scripts, puede posponer el reinicio hasta que se realice todo el trabajo de configuración.

## <a name="post-install-configuration"></a>Configuración posterior a la instalación

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Una vez finalizada la instalación, reinicie el servicio y, a continuación, configure el servidor para habilitar la ejecución del script:

+ [Habilitación de la ejecución de scripts externos](sql-machine-learning-services-windows-install.md#bkmk_enableFeature)

Una instalación sin conexión inicial de SQL Server Machine Learning Services requiere la misma configuración que una instalación en línea:

+ [Comprobación de la instalación](sql-machine-learning-services-windows-install.md#verify-installation)
+ [Configuración adicional según sea necesario](sql-machine-learning-services-windows-install.md#additional-configuration)
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Una vez finalizada la instalación, reinicie el servicio y, a continuación, configure el servidor para habilitar la ejecución del script:

+ [Habilitación de la ejecución de scripts externos](sql-r-services-windows-install.md#bkmk_enableFeature)

Una instalación sin conexión inicial de SQL Server R Services requiere la misma configuración que una instalación en línea:

+ [Comprobación de la instalación](sql-r-services-windows-install.md#verify-installation)
+ [Configuración adicional según sea necesario](sql-r-services-windows-install.md#bkmk_FollowUp)
::: moniker-end

## <a name="next-steps"></a>Pasos siguientes

Para comprobar el estado de la instalación de la instancia y corregir problemas comunes, consulte [Informes personalizados para SQL Server](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

Para obtener ayuda con mensajes o entradas de registro desconocidos, consulte [Preguntas más frecuentes sobre actualización e instalación: Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).
