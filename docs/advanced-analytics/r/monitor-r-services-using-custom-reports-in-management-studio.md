---
title: 'Supervisar R Services con informes personalizados en Management Studio: SQL Server Machine Learning Services'
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 71a8e0adf814128e78651b43ad14a43fc231f87c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962587"
---
# <a name="monitor-machine-learning-services-using-custom-reports-in-management-studio"></a>Supervisar Machine Learning Services con informes personalizados en Management Studio
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Para que sea más fácil de administrar la instancia utilizada para el aprendizaje automático, el equipo del producto ha ofrecido una serie de informes personalizado de ejemplo que se pueden agregar a SQL Server Management Studio. En estos informes, puede ver detalles tales como:

- Sesiones activa R o Python
- Configuración de la instancia
- Estadísticas de ejecución de trabajos de machine learning
- Eventos extendidos para R Services
- Paquetes de R o Python instalados en la instancia actual

En este artículo se explica cómo instalar y usar los informes personalizados proporcionados específicamente para la máquina leaerning. 

Para obtener una introducción general a los informes en Management Studio, consulte [informes personalizados en Management Studio](../../ssms/object/custom-reports-in-management-studio.md).

## <a name="how-to-install-the-reports"></a>Cómo instalar los informes

Los informes se diseñan mediante SQL Server Reporting Services, pero pueden utilizarse directamente desde SQL Server Management Studio, incluso aunque Reporting Services no esté instalado en la instancia. 

Para utilizar estos informes:

* Descargue los archivos RDL desde el repositorio de GitHub para obtener ejemplos de productos de SQL Server.
* Agregue los archivos a la carpeta de informes personalizados utilizada por SQL Server Management Studio.
* Abra los informes en SQL Server Management Studio.


### <a name="step-1-download-the-reports"></a>Paso 1. Descargar los informes

1. Abra el repositorio de GitHub que contiene [muestras de productos de SQL Server](https://github.com/Microsoft/sql-server-samples)y descargar los informes de ejemplo. 

    + [Informes personalizados de SSMS](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports)

    > [!NOTE]
    > Los informes se pueden usar con servicios de aprendizaje de máquina de SQL Server 2017 o SQL Server 2016 R Services.

2. Para descargar los ejemplos, también puede iniciar sesión en GitHub y realizar una bifurcación local de los ejemplos. 

### <a name="step-2-copy-the-reports-to-management-studio"></a>Paso 2. Copiar los informes en Management Studio

3. Ubique la carpeta de informes personalizados utilizada por SQL Server Management Studio. De forma predeterminada, los informes personalizados se almacenan en esta carpeta:
    
   `C:\Users\user_name\Documents\SQL Server Management Studio\Custom Reports`

   Sin embargo, puede especificar una carpeta diferente o crear subcarpetas.

4. Copie los archivos *.RDL en la carpeta de informes personalizados.


### <a name="step-3-run-the-reports"></a>Paso 3. Ejecutar los informes

5. En Management Studio, haga clic en el nodo **Bases de datos** de la instancia donde quiere ejecutar los informes.
6. Haga clic en **Informes**y, después, en **Informes personalizados**.
7. En el cuadro de diálogo **Abrir archivo** , ubique la carpeta de informes personalizados.
8. Seleccione uno de los archivos RDL que descargó y, luego, haga clic en **Abrir**.

> [!IMPORTANT]
> En algunos equipos, como los dispositivos con pantallas con valores altos de PPP o una resolución superior a 1080p, en algunas sesiones de escritorio remoto, no se pueden utilizar estos informes. Hay un error en el control de visor de informes en SSMS que se bloquea el informe.

## <a name="report-list"></a>Lista de informes

Actualmente, el repositorio de ejemplos del producto en GitHub incluye los siguientes informes:

+ **R Services: sesiones activas**

  Use este informe para ver los usuarios que están conectados actualmente a la instancia de SQL Server y la máquina en ejecución trabajos de aprendizaje. 
  
+ **R Services: configuración**

  Use este informe para ver la configuración del tiempo de ejecución de scripts externos y servicios relacionados. El informe indicará si es necesario un reinicio y buscará los protocolos de red necesarios. 
  
  Autenticación implícita es necesaria para tareas de aprendizaje automático que se ejecutan en SQL Server como un contexto de proceso. Para comprobar que la autenticación implícita está configurada, el informe comprueba si existe un inicio de sesión de base de datos para el grupo SQLRUserGroup.

 + **R Services : configuración de una instancia** 

   Este informe está pensado para ayudarle a configurar el aprendizaje automático. También puede ejecutar este informe para corregir errores de configuración que se encuentra en el informe anterior.
 
+ **R Services: estadísticas de ejecución**

  Use este informe para ver estadísticas de ejecución de trabajos de machine learning. Por ejemplo, puede obtener el número total de secuencias de comandos de R que se han ejecutado, el número de ejecuciones en paralelo y las funciones RevoScaleR utilizadas con más frecuencia. Haga clic en **ver Script de SQL** para obtener el código de T-SQL completo detrás de este informe.

  Actualmente el informe solo supervisa estadísticas para las funciones del paquete de RevoScaleR.

+ **R Services: eventos extendidos**

  Utilice este informe para ver una lista de los eventos extendidos que están disponibles para supervisar las tareas relacionadas con los tiempos de ejecución del script externo. Haga clic en **ver Script de SQL** para obtener el código de T-SQL completo detrás de este informe.

+ **R Services: paquetes**

  Use este informe para ver una lista de los paquetes de R o Python instalados en la instancia de SQL Server.

+ **R Services: uso de recursos**

  Use este informe para ver el consumo de recursos de CPU, memoria y E/S por ejecución de scripts externos. También puede ver la configuración de la memoria de grupos de recursos externos.

## <a name="see-also"></a>Vea también

[Servicios de supervisión](managing-and-monitoring-r-solutions.md)

[Eventos extendidos para R Services](extended-events-for-sql-server-r-services.md)
