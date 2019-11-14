---
title: Configurar la reproducción para las actualizaciones de SQL Server
description: Configurar la reproducción en Asistente para experimentación con bases de datos
ms.custom: seo-lt-2019
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
ms.openlocfilehash: b58233e40e27908f0bc8b03a95455216de2c119c
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056717"
---
# <a name="configure-replay-in-database-experimentation-assistant"></a>Configurar la reproducción en Asistente para experimentación con bases de datos

Asistente para experimentación con bases de datos (DEA) utiliza las herramientas de Distributed Replay de la instalación de SQL Server para reproducir un seguimiento capturado en un entorno de prueba actualizado. Se recomienda realizar una serie de pruebas usando un archivo de seguimiento pequeño antes de realizar una reproducción completa para garantizar la reproducción correcta de las consultas.

## <a name="distributed-replay-requirements"></a>Requisitos de Distributed Replay

- Se requiere un 78% adicional de espacio en disco duro para crear archivos IRF en la máquina del controlador de Distributed Replay.
- 200 MB o 512 MB es el tamaño de sustitución de seguimiento ideal que se va a usar para capturar seguimientos de producción o de rendimiento.   
- Los requisitos mínimos de CPU y RAM para el controlador de Distributed Replay y los equipos cliente son una CPU de un solo núcleo con 3,5 GB de RAM.
- El tiempo de reproducción tarda aproximadamente 1,55 veces más que el tiempo de captura porque se usan un controlador y cuatro equipos secundarios para reproducir el seguimiento de producción.
- Si usa nuestras versiones "publicadas" de los archivos de definición de seguimiento de rendimiento y producción, y la definición de seguimiento de rendimiento filtra los seguimientos de una base de datos de interés, el análisis muestra que el tamaño del **seguimiento de rendimiento** es aproximadamente 15 veces mayor que el tamaño de **seguimiento de producción** .

## <a name="set-up-a-virtual-network-or-domain"></a>Configuración de una red virtual o un dominio

Distributed Replay requiere el uso de cuentas comunes entre equipos. Debido a este requisito, y por motivos de seguridad, se recomienda ejecutar Distributed Replay en una red virtual o en una red controlada por dominio:

- Cree el controlador y los equipos cliente en el entorno.
- Asegúrese de que el controlador y los equipos cliente pueden hacer ping entre sí a través de la red.
- Distributed Replay equipos cliente deben tener conectividad con el equipo de destino de reproducción que ejecuta SQL Server.

## <a name="set-up-the-controller-service"></a>Configurar el servicio del controlador

Para configurar el servicio del controlador:

1. Instale el controlador de Distributed Replay mediante el instalador de SQL Server. Si omitió el paso del Asistente para SQL Server Installer que configura el controlador de Distributed Replay, puede configurar el controlador mediante el archivo de configuración. En una instalación típica, el archivo de configuración se encuentra en C:\Archivos de programa (x86) \Microsoft SQL Server\<versión\>\Tools\DReplayController\DReplayController.config.
1. Los registros del controlador de Distributed Replay se encuentran en C:\Archivos de programa (x86) \Microsoft SQL Server\<versión\>\Tools\DReplayController\Log.
1. Abra Services. msc y vaya al servicio de **controlador de Distributed Replay de SQL Server** .
1. Haga clic con el botón secundario en el servicio y, a continuación, seleccione **propiedades**. Establezca la cuenta de servicio en una cuenta que sea común a las máquinas cliente y del controlador de la red.
1. Seleccione **Aceptar** para cerrar la ventana **propiedades** .
1. Reinicie el servicio del **controlador de SQL Server Distributed Replay** desde Services. msc. También puede ejecutar los siguientes comandos en la línea de comandos para reiniciar el servicio:<br/>
   `NET STOP "SQL Server Distributed Replay Controller"`<br/>
   `NET START "SQL Server Distributed Replay Controller"`
1. Para más opciones de configuración, consulte [configuración de Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/configure-distributed-replay).

## <a name="configure-dcom"></a>Configurar DCOM

Esta configuración solo es necesaria en el equipo del controlador.

1. Abra DCOMCNFG. exe.
1. Expanda **servicios de componentes** > **equipos** > **mi PC** > **Configuración DCOM**.
1. En **Configuración DCOM**, haga clic con el botón secundario en **DReplayController**y seleccione **propiedades**.
1. Seleccione la pestaña **Seguridad** .
1. En **permisos de inicio y activación**, seleccione **personalizar**y, a continuación, seleccione **Editar**.
1. Agregue el usuario que va a iniciar la reproducción. Conceda al usuario el inicio local y los permisos de activación local. Si el usuario tiene previsto iniciar o activar de forma remota, conceda al usuario permisos de inicio remoto y activación remota.
1. Seleccione **Aceptar** para confirmar los cambios y volver a la pestaña **seguridad** .
1. En **permisos de acceso**, seleccione **personalizar**y, a continuación, seleccione **Editar**.
1. Agregue el usuario que va a iniciar la reproducción. Conceda a los permisos de acceso local del usuario. Si el usuario tiene previsto tener acceso al servicio de controlador de forma remota, conceda a los usuarios permisos de acceso remoto.
1. Seleccione **Aceptar** para confirmar los cambios y volver a la pestaña **seguridad** .
1. Seleccione **Aceptar** para confirmar los cambios.
1. Reinicie el servicio del controlador de SQL Server Distributed Replay desde Services. msc. También puede ejecutar los siguientes comandos en la línea de comandos para reiniciar el servicio:<br/>
   `NET STOP "SQL Server Distributed Replay Controller"`<br/>
   `NET START "SQL Server Distributed Replay Controller"`

## <a name="set-up-the-client-service"></a>Configurar el servicio de cliente

Antes de configurar el servicio de cliente, use herramientas de red como ping para comprobar que el controlador y los equipos cliente pueden comunicarse.

1. Instale el cliente de Distributed Replay mediante el instalador de SQL Server.
1. Abra Services. msc y vaya al servicio de cliente de SQL Server Distributed Replay.
1. Haga clic con el botón secundario en el servicio y, a continuación, seleccione **propiedades**. Establezca la cuenta de servicio en una cuenta que sea común a los equipos del controlador y del cliente de la red.
1. Seleccione **Aceptar** para cerrar la ventana **propiedades** . Si omitió el paso del Asistente para SQL Server Installer para configurar el cliente de Distributed Replay, puede configurarlo mediante el archivo de configuración. En una instalación típica, el archivo de configuración se encuentra en C:\Archivos de programa (x86) \Microsoft SQL Server\<versión\>\Tools\DReplayClient\DReplayClient.config.
1. Asegúrese de que el archivo DReplayClient. config contiene el nombre del equipo del controlador como su controlador para el registro.
1.  Reinicie el servicio de cliente de SQL Server Distributed Replay desde Services. msc. También puede ejecutar los siguientes comandos desde la línea de comandos para reiniciar el servicio:<br/>
    `NET STOP "SQL Server Distributed Replay Client"`<br/>
    `NET START "SQL Server Distributed Replay Client"`
1. Los registros del controlador de Distributed Replay se encuentran en C:\Archivos de programa (x86) \Microsoft SQL Server\<versión\>\Tools\DReplayClient\Log. Los registros indican si el cliente se puede registrar a sí mismo con el controlador.
1. Si la configuración es correcta, el registro muestra el mensaje "registrado con el controlador < el nombre del controlador\>".
1. Para más opciones de configuración, consulte [configuración de Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/configure-distributed-replay).

## <a name="set-up-distributed-replay-administration-tools"></a>Configurar herramientas de administración de Distributed Replay

Puede usar Distributed Replay herramientas de administración para probar rápidamente si Distributed Replay funciona correctamente en el entorno. La prueba de la configuración puede ser especialmente útil en un entorno en el que se registran varios equipos cliente con un controlador. Es posible que tenga que instalar SQL Server Management Studio (SSMS) para obtener las herramientas de administración.

1. Vaya a la ubicación de instalación de SSMS y busque la herramienta de administración de Distributed Replay dreplay. exe y sus componentes dependientes.
1. Abra una ventana del símbolo del sistema y ejecute `dreplay.exe status -f 1`.
1. Si todos los pasos anteriores son correctos, la salida de la consola indica que el controlador puede ver sus clientes en un estado de `READY`.

## <a name="configure-the-firewall-for-remote-distributed-replay-access"></a>Configurar el firewall para el acceso de Distributed Replay remoto

El acceso remoto a Distributed Replay requiere la apertura de puertos visibles en el dominio o en la red virtual.

1. Abra **firewall de Windows** con **seguridad avanzada**.
1. Vaya a **reglas de entrada**.
1. Cree una nueva regla de Firewall de entrada para el programa C:\Program Files (x86) \Microsoft SQL Server\<versión\>\Tools\DReplayController\DReplayController.exe.
1. Permitir el acceso de nivel de dominio a todos los puertos de DReplayController. exe para poder comunicarse con el servicio de controlador de forma remota.
1. Guarde la regla.

## <a name="set-up-target-computers"></a>Configuración de equipos de destino

Se necesitan dos supeticiones para ejecutar una prueba A/B o un experimento. Es decir, es posible que necesite dos instancias independientes de instalaciones SQL Server para un escenario de migración. 

También puede instalar las dos versiones de SQL Server instancias en el mismo equipo. Una advertencia es asegurarse de que las instancias están completamente aisladas cuando una reproducción está en curso.

Se deben realizar los pasos siguientes para cada reproducción:

1. Restaure la copia de seguridad de la base de datos.
1. Proporcione permisos para que el usuario de la cuenta de servicio del cliente tenga acceso a las bases de datos en la instancia de SQL Server. Los permisos son necesarios para que las consultas se ejecuten en la instancia de SQL Server.
1. Inicie la reproducción.

## <a name="next-steps"></a>Pasos siguientes

- Para obtener información sobre cómo reproducir un seguimiento capturado en un entorno de prueba actualizado, vea [reproducción de seguimiento](database-experimentation-assistant-replay-trace.md).

- Para obtener una introducción de 19 minutos a DEA y demostraciones, vea el siguiente vídeo:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
