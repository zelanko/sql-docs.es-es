---
title: 'Instalar el lenguaje R y componentes de Python sin acceso a internet: SQL Server Machine Learning'
description: Sin conexión o desconectada R de Machine Learning y Python el programa de instalación en una instancia de SQL Server aislado detrás de un firewall de red.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: c14f6c3c404cee8a4197672c851cf1358b9a8d9b
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511922"
---
# <a name="install-sql-server-machine-learning-r-and-python-on-computers-with-no-internet-access"></a>Instalar SQL Server de aprendizaje automático R y Python en equipos sin acceso a internet
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

De forma predeterminada, los instaladores de conecten a sitios de descarga de Microsoft para obtener necesarios y los componentes actualizados para aprendizaje automático en SQL Server. Si las restricciones de firewall impide que el instalador de llegar a estos sitios, puede usar un dispositivo conectado a internet para descargar archivos, transferir archivos a un servidor sin conexión y, a continuación, ejecute el programa de instalación.

Análisis en bases de datos constan de instancia del motor de base de datos, además de otros componentes de integración de R y Python, según la versión de SQL Server. 

+ SQL Server 2017 incluye R y Python 
+ SQL Server 2016 es solo para R.

En un servidor aislado, aprendizaje automático y las características específicas del lenguaje de R o Python se agregan a través de los archivos CAB. 

## <a name="sql-server-2017-offline-install"></a>Instalación sin conexión de SQL Server 2017

Para instalar SQL Server 2017 Machine Learning Services (R y Python) en un servidor aislado, comience por descargar la versión inicial de SQL Server y compatibilidad con los correspondientes archivos CAB de R y Python. Incluso si tiene previsto actualizar inmediatamente el servidor para usar la actualización acumulativa más reciente, primero debe instalarse una versión inicial.

> [!Note]
> SQL Server 2017 no tiene los service packs. Es la primera versión de SQL Server para usar la versión inicial como la única línea de base, con el mantenimiento de las actualizaciones acumulativas solo. 

### <a name="1---download-2017-cabs"></a>1: descargar archivos CAB de 2017

En un equipo que tiene una conexión a internet, descargue los archivos CAB que proporciona funciones de R y Python para la versión inicial y los medios de instalación de SQL Server 2017. 

Versión  |Vínculo de descarga  |
---------|---------------|
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Apertura de Python de Microsoft     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Microsoft Python Server    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |

###  <a name="2---get-sql-server-2017-installation-media"></a>2 - obtener medios de instalación de SQL Server 2017

1. En un equipo que tiene una conexión a internet, descargue el [programa de instalación de SQL Server 2017](https://www.microsoft.com/sql-server/sql-server-downloads). 

2. Haga doble clic en el programa de instalación y elija el **descargar medios** tipo de instalación. Con esta opción, el programa de instalación crea un archivo .iso (o .cab) local que contiene el medio de instalación.

   ![Elegir tipo de instalación de los medios de descarga](media/offline-download-tile.png "descargar archivos multimedia")

## <a name="sql-server-2016-offline-install"></a>Instalación sin conexión de SQL Server 2016

Análisis en bases de datos de SQL Server 2016 es sólo R, con sólo dos CAB los archivos de paquetes de productos y la distribución de Microsoft de R de código abierto, respectivamente. Comience por instalar cualquiera de estas versiones: RTM, SP 1, SP 2. Una vez que una instalación básica está en su lugar, se pueden aplicar las actualizaciones acumulativas como paso siguiente.

En un equipo que tiene una conexión a internet, descargue los archivos CAB que se usa el programa de instalación para instalar el análisis en bases de datos en SQL Server 2016. 

### <a name="1---download-2016-cabs"></a>1: descargar archivos CAB de 2016

Versión  | Microsoft R Open | Microsoft R Server |
---------|-----------------|---------------------|
**SQL Server 2016 RTM**     | [SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266) |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051) |
**SQL Server 2016 SP 1**     | [SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879) |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881) | 
**SQL Server 2016 SP 2**  |[SRO_3.2.2.20000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866039) |[SRS_8.0.3.20000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866038) |

### <a name="2---get-sql-server-2016-installation-media"></a>2 - obtener medios de instalación de SQL Server 2016

Puede instalar SQL Server 2016 RTM, Service Pack 1 o Service Pack 2 como la primera instalación en el equipo de destino. Cualquiera de estas versiones puede aceptar una actualización acumulativa.

Es una manera de obtener un archivo .iso que contiene el medio de instalación a través de [Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/). Inicie sesión y, a continuación, utilice el **descargas** vínculo para buscar la versión de SQL Server 2016 que desea instalar. La descarga está en forma de un archivo .iso, que puede copiar en el equipo de destino para una instalación sin conexión.

## <a name="transfer-files"></a>Transferencia de archivos

Copie los medios de instalación de SQL Server (.iso o .cab) y los archivos de análisis en bases de datos CAB en el equipo de destino. Coloque los archivos CAB y el archivo de medios de instalación en la misma carpeta en el equipo de destino, como la carpeta TEMP * % del usuario del programa de instalación.

Falta la carpeta % TEMP % para los archivos CAB de Python. Para R, puede usar % TEMP % o establezca el parámetro de myrcachedirectory en la ruta de acceso del archivo CAB.

Captura de pantalla siguiente muestra los archivos CAB de SQL Server 2017 e ISO. Descargas de SQL Server 2016 tienen un aspecto distintas: es el nombre de archivo menos archivos (sin Python) y los medios de instalación para 2016.

![Lista de archivos que se transferirá](media/offline-file-list.png "lista de archivos")

## <a name="run-setup"></a>Ejecute el programa de instalación

Al ejecutar el programa de instalación de SQL Server en un equipo conectado a internet, el programa de instalación agrega un **instalación sin conexión** paginar en el Asistente para que pueda especificar la ubicación de los archivos .cab que copió en el paso anterior.

1. Para comenzar la instalación, haga doble clic en el archivo .iso o .cab para tener acceso a los medios de instalación. Debería ver el **setup.exe** archivo.

2. Haga clic en **setup.exe** y ejecutar como administrador.

3. Cuando el Asistente para la instalación muestra la página de licencia para componentes de R o Python de código abierto, haga clic en **Accept**. Aceptación de términos de licencia le permite continuar con el paso siguiente.

4. Cuando llegue a la **instalación sin conexión** página **ruta de instalación**, especifique la carpeta que contiene los archivos CAB que copió anteriormente.

   ![Página del Asistente para la selección de carpeta cab](media/screenshot-sql-offline-cab-page.png "carpeta CAB")

5. Continuar siguientes las indicaciones en pantalla para completar la instalación.

<a name="apply-cu"></a>

## <a name="apply-cumulative-updates"></a>Aplicar actualizaciones acumulativas

Se recomienda que aplique la actualización acumulativa más reciente para el motor de base de datos y los componentes de aprendizaje automático. Las actualizaciones acumulativas se instalan a través del programa de instalación. 

1. Comience con una instancia de la línea base. Solo se pueden aplicar las actualizaciones acumulativas para las instalaciones existentes de SQL Server:

  + Versión inicial de SQL Server 2017
  + Versión inicial de SQL Server 2016, SQL Server 2016 Service Pack 1 o SQL Server 2016 Service Pack 2

2. En un dispositivo conectado a internet, vaya a la lista de actualizaciones acumulativas para su versión de SQL Server:

  + [Actualizaciones de SQL Server 2017](https://sqlserverupdates.com/sql-server-2017-updates/)
  + [Actualizaciones de SQL Server 2016](https://sqlserverupdates.com/sql-server-2016-updates/)

3. Seleccione la actualización acumulativa más reciente para descargar el archivo ejecutable.

4. Obtener archivos CAB correspondientes para R y Python. Para obtener vínculos de descarga, vea [CAB descargas para las actualizaciones acumulativas en el análisis en bases de datos de SQL Server en instancias](sql-ml-cab-downloads.md).

5. Transferir todos los archivos, archivos ejecutables y CAB, en la misma carpeta en el equipo sin conexión.

6. Ejecute el programa de instalación. Acepte los términos de licencia y, en la página de selección de características, revise las características para el que se aplican las actualizaciones acumulativas. Debería ver todas las características instaladas para la instancia actual, incluidas características de aprendizaje automático.

  ![Seleccione las características en el árbol de características](media/cumulative-update-feature-selection.png "lista de características")

5. Continúe con el asistente, acepte los términos de licencia para las distribuciones de R y Python. Durante la instalación, deberá elegir la ubicación de la carpeta que contiene los archivos CAB actualizados.

## <a name="set-environment-variables"></a>Establezca variables de entorno

Para solo integración de características de R, se debe establecer el **MKL_CBWR** variable de entorno [garantizar resultados coherentes](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) de cálculos de Intel Math Kernel Library (MKL).

1. En el Panel de Control, haga clic en **sistema y seguridad** > **sistema** > **configuración avanzada del sistema**  >   **Las Variables de entorno**.

2. Crear una nueva variable de usuario o del sistema. 

  + Establezca el nombre de variable en `MKL_CBWR`
  + Establece el valor de la variable en `AUTO`

Este paso requiere un reinicio del servidor. Si va a habilitar la ejecución del script, puede contener en el reinicio hasta que se hace todo el trabajo de configuración.

## <a name="post-install-configuration"></a>Configuración posterior a la instalación

Una vez finalizada la instalación, reinicie el servicio y, a continuación, configure el servidor para habilitar la ejecución del script:

+ [Habilitar la ejecución de scripts externos (SQL Server 2017)](sql-machine-learning-services-windows-install.md#bkmk_enableFeature)
+ [Habilitar la ejecución de scripts externos (SQL Server 2016)](sql-r-services-windows-install.md#bkmk_enableFeature)

Una instalación sin conexión inicial de SQL Server 2017 Machine Learning Services o SQL Server 2016 R Services requiere la misma configuración que una instalación en línea:

+ [Comprobar la instalación](sql-machine-learning-services-windows-install.md#verify-installation) (para SQL Server 2016, haga clic en [aquí](sql-r-services-windows-install.md#verify-installation)).
+ [Configuración adicional según sea necesario](sql-machine-learning-services-windows-install.md#additional-configuration) (para SQL Server 2016, haga clic en [aquí](sql-r-services-windows-install.md#bkmk_FollowUp)).

## <a name="next-steps"></a>Pasos siguientes

Para comprobar el estado de instalación de la instancia y corregir los problemas comunes, consulte [informes personalizados para SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

Para obtener ayuda con todos los mensajes no conocidos o las entradas del registro, consulte [actualización e instalación preguntas más frecuentes - Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).

