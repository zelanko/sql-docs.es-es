---
title: Instalación de componentes de idioma y Python de R sin acceso a Internet
description: Sin conexión o desconectado Machine Learning el programa de instalación de R y Python en una instancia aislada de SQL Server detrás de un firewall de red.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ddeea99addae3229575ca581f344332587e85981
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715822"
---
# <a name="install-sql-server-machine-learning-r-and-python-on-computers-with-no-internet-access"></a>Instalación de SQL Server machine learning R y Python en equipos sin acceso a Internet
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

De forma predeterminada, los instaladores se conectan a sitios de descarga de Microsoft para obtener los componentes necesarios y actualizados del aprendizaje automático en SQL Server. Si las restricciones de Firewall impiden que el instalador alcance estos sitios, puede usar un dispositivo conectado a Internet para descargar archivos, transferir archivos a un servidor sin conexión y, a continuación, ejecutar el programa de instalación.

El análisis en base de datos consta de una instancia del motor de base de datos, además de componentes adicionales para la integración de R y Python, dependiendo de la versión de SQL Server. 

+ SQL Server 2017 y versiones posteriores incluyen R y Python 
+ SQL Server 2016 es de solo lectura.

En un servidor aislado, las características específicas del lenguaje de R/Python y aprendizaje automático se agregan a través de archivos. CAB. 

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="sql-server-2017-offline-install"></a>Instalación sin conexión de SQL Server 2017

Para instalar SQL Server Machine Learning Services (R y Python) en un servidor aislado, empiece por descargar la versión inicial de SQL Server y los archivos. CAB correspondientes para la compatibilidad con R y Python. Incluso si planea actualizar inmediatamente el servidor para que use la actualización acumulativa más reciente, primero se debe instalar una versión inicial.

> [!Note]
> SQL Server 2017 no tiene Service Packs. Es la primera versión de SQL Server de usar la versión inicial como única línea base, con mantenimiento solo a través de las actualizaciones acumulativas. 

### <a name="1---download-2017-cabs"></a>1-Descargar 2017 CAB

En un equipo que tenga una conexión a Internet, descargue los archivos. CAB que proporcionan las características de R y Python para la versión inicial y los medios de instalación de SQL Server 2017. 

Release  |Vínculo de descarga  |
---------|---------------|
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Microsoft Python abierto     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Microsoft Python Server    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |

###  <a name="2---get-sql-server-2017-installation-media"></a>2-obtener medios de instalación de SQL Server 2017

1. En un equipo que tenga una conexión a Internet, descargue el [programa de instalación de SQL Server 2017](https://www.microsoft.com/sql-server/sql-server-downloads). 

2. Haga doble clic en configuración y elija el tipo de instalación **Descargar medios** . Con esta opción, el programa de instalación crea un archivo local. ISO (o. cab) que contiene el medio de instalación.

   ![Elija el tipo de instalación descargar medio](media/offline-download-tile.png "Descargar medios")

::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

## <a name="sql-server-2016-offline-install"></a>Instalación sin conexión de SQL Server 2016

SQL Server 2016 análisis en base de datos es de solo lectura, con solo dos archivos CAB para paquetes de productos y la distribución de Microsoft de código abierto, respectivamente. Empiece por instalar cualquiera de estas versiones: RTM, SP 1, SP 2. Una vez que se realiza una instalación base, las actualizaciones acumulativas se pueden aplicar como paso siguiente.

En un equipo que tenga una conexión a Internet, descargue los archivos. CAB utilizados por el programa de instalación para instalar el análisis de base de datos en SQL Server 2016. 

### <a name="1---download-2016-cabs"></a>1-Descargar 2016 CAB

Release  | Microsoft R Open | Microsoft R Server |
---------|-----------------|---------------------|
**SQL Server 2016 RTM**     | [SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266) |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051) |
**SQL Server 2016 SP 1**     | [SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879) |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881) | 
**SQL Server 2016 SP 2**  |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866039) |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317) |

### <a name="2---get-sql-server-2016-installation-media"></a>2-obtener medios de instalación de SQL Server 2016

Puede instalar SQL Server 2016 RTM, SP 1 o SP 2 como primera instalación en el equipo de destino. Cualquiera de estas versiones puede aceptar una actualización acumulativa.

Una manera de obtener un archivo. ISO que contiene el medio de instalación se realiza a través de [Visual Studio dev Essentials](https://visualstudio.microsoft.com/dev-essentials/). Inicie sesión y, a continuación, use el vínculo downloads para encontrar la versión SQL Server 2016 que desea instalar. La descarga está en forma de un archivo. ISO, que puede copiar en el equipo de destino para una instalación sin conexión.

::: moniker-end

## <a name="transfer-files"></a>Transferir archivos

Copie el disco de instalación de SQL Server (. ISO o. cab) y los archivos. CAB de análisis en la base de datos en el equipo de destino. Coloque los archivos. CAB y el archivo de medios de instalación en la misma carpeta del equipo de destino, como la carpeta% TEMP * del usuario de la instalación.

La carpeta% TEMP% es necesaria para los archivos. CAB de Python. Para R, puede usar% TEMP% o establecer el parámetro myrcachedirectory en la ruta de acceso del archivo. CAB.

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
En la captura de pantalla siguiente se muestra SQL Server archivos CAB e ISO. 

![Lista de archivos que se van a transferir](media/offline-file-list.png "Lista de archivos")
::: moniker-end

## <a name="run-setup"></a>Ejecutar el programa de instalación

Al ejecutar el programa de instalación de SQL Server en un equipo desconectado de Internet, el programa de instalación agrega una página de **instalación sin conexión** al Asistente para que pueda especificar la ubicación de los archivos. cab que copió en el paso anterior.

1. Para comenzar la instalación, haga doble clic en el archivo. ISO o. cab para tener acceso a los medios de instalación. Debería ver el archivo **setup. exe** .

2. Haga clic con el botón secundario en **setup. exe** y ejecute como administrador.

3. Cuando el Asistente para la instalación muestre la página de licencias de componentes de R o Python de código abierto, haga clic en **Aceptar**. La aceptación de los términos de licencia le permite continuar con el siguiente paso.

4. Cuando llegue a la página de **instalación sin conexión** , en **ruta de acceso de instalación**, especifique la carpeta que contiene los archivos. cab que copió anteriormente.

   ![Página del Asistente para la selección de la carpeta CAB](media/screenshot-sql-offline-cab-page.png "Carpeta CAB")

5. Siga las indicaciones en pantalla para completar la instalación.

<a name="apply-cu"></a>

## <a name="apply-cumulative-updates"></a>Aplicar actualizaciones acumulativas

Se recomienda aplicar la última actualización acumulativa al motor de base de datos y a los componentes de aprendizaje automático. Las actualizaciones acumulativas se instalan a través del programa de instalación. 

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
1. Comience con una instancia de línea de base. Solo puede aplicar las actualizaciones acumulativas a las instalaciones existentes de la versión inicial de SQL Server.

2. En un dispositivo conectado a Internet, vaya a la lista de actualizaciones acumulativas correspondiente a su versión de SQL Server:

  + [SQL Server 2017 actualizaciones](https://sqlserverupdates.com/sql-server-2017-updates/)
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
1. Comience con una instancia de línea de base. Solo puede aplicar actualizaciones acumulativas a las instalaciones existentes de la versión SQL Server 2016 inicial, SQL Server 2016 SP 1 o SQL Server 2016 SP 2.

2. En un dispositivo conectado a Internet, vaya a la lista de actualizaciones acumulativas correspondiente a su versión de SQL Server:

  + [SQL Server 2016 actualizaciones](https://sqlserverupdates.com/sql-server-2016-updates/)
::: moniker-end

3. Seleccione la actualización acumulativa más reciente para descargar el archivo ejecutable.

4. Obtiene los archivos. CAB correspondientes para R y Python. Para obtener vínculos de descarga, consulte [descargas de CAB para actualizaciones acumulativas en SQL Server instancias de análisis en base de datos](sql-ml-cab-downloads.md).

5. Transfiera todos los archivos, archivos ejecutables y archivos. CAB a la misma carpeta del equipo sin conexión.

6. Ejecute el programa de instalación. Acepte los términos de licencia y, en la página selección de características, revise las características para las que se aplican las actualizaciones acumulativas. Debería ver todas las características instaladas para la instancia actual, incluidas las características de aprendizaje automático.

    ![Seleccionar características en el árbol de características](media/cumulative-update-feature-selection.png "lista de características")

5. Continúe con el asistente y acepte los términos de licencia para las distribuciones de R y Python. Durante la instalación, se le pedirá que elija la ubicación de la carpeta que contiene los archivos. CAB actualizados.

## <a name="set-environment-variables"></a>Establecer variables de entorno

Solo para la integración de características de R, debe establecer la variable de entorno **MKL_CBWR** para [garantizar una salida coherente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) de los cálculos de la biblioteca de kernels matemáticos (MKL) de Intel.

1. En el panel de control, haga clic en sistema **y seguridad** >  > **configuración** > avanzada del sistema**variables de entorno**.

2. Cree una nueva variable de usuario o del sistema. 

  + Establezca el nombre de la variable en`MKL_CBWR`
  + Establezca el valor de la variable en`AUTO`

Este paso requiere un reinicio del servidor. Si va a habilitar la ejecución de scripts, puede mantener el reinicio hasta que se realice todo el trabajo de configuración.

## <a name="post-install-configuration"></a>Configuración posterior a la instalación

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Una vez finalizada la instalación, reinicie el servicio y, a continuación, configure el servidor para habilitar la ejecución del script:

+ [Habilitar la ejecución de scripts externos](sql-machine-learning-services-windows-install.md#bkmk_enableFeature)

Una instalación sin conexión inicial de SQL Server Machine Learning Services requiere la misma configuración que una instalación en línea:

+ [Comprobar la instalación](sql-machine-learning-services-windows-install.md#verify-installation)
+ [Configuración adicional según sea necesario](sql-machine-learning-services-windows-install.md#additional-configuration)
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Una vez finalizada la instalación, reinicie el servicio y, a continuación, configure el servidor para habilitar la ejecución del script:

+ [Habilitar la ejecución de scripts externos](sql-r-services-windows-install.md#bkmk_enableFeature)

Una instalación sin conexión inicial de SQL Server R Services requiere la misma configuración que una instalación en línea:

+ [Comprobar la instalación](sql-r-services-windows-install.md#verify-installation)
+ [Configuración adicional según sea necesario](sql-r-services-windows-install.md#bkmk_FollowUp)
::: moniker-end

## <a name="next-steps"></a>Pasos siguientes

Para comprobar el estado de la instalación de la instancia y corregir los problemas comunes, vea [informes personalizados para SQL Server](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

Para obtener ayuda con mensajes o entradas de registro desconocidos, consulte [preguntas más frecuentes Machine Learning Services sobre actualización e instalación](../r/upgrade-and-installation-faq-sql-server-r-services.md).
