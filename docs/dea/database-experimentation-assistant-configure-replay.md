---
title: Configurar reproducción en el Asistente de experimentación de base de datos para las actualizaciones de SQL Server
description: Configuración de reproducción en el Asistente de experimentación de base de datos
ms.custom: ''
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: 76516c02b03443ca6c7642f75c16cf53b07b3e8a
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2018
ms.locfileid: "56987791"
---
# <a name="configure-replay-in-database-experimentation-assistant"></a>Configuración de reproducción en el Asistente de experimentación de base de datos

Ayudante para la base de datos de experimentación (DEA) usa las herramientas de Distributed Replay desde la instalación de SQL Server para reproducir un seguimiento capturado contra un entorno de pruebas actualizado. Se recomienda realizar una ejecución mediante el uso de un archivo de seguimiento pequeño antes de realizar una reproducción completa para garantizar una reproducción adecuada de las consultas de prueba.

## <a name="distributed-replay-requirements"></a>Requisitos de reproducción distribuidos

- Se requiere un 78% más de espacio en disco duro para crear archivos IRF en la máquina del controlador de Distributed Replay.
- 200 MB o 512 MB es el tamaño de sustitución incremental de seguimiento ideal para capturar seguimientos de rendimiento o de producción.   
- Los requisitos mínimos de CPU y RAM para las máquinas de controlador y el cliente de Distributed Replay son una CPU de núcleo único con 3,5 GB de RAM.
- El tiempo de reproducción tarda aproximadamente 1,55 veces a la hora de captura porque un controlador y cuatro equipos secundarios se usan para reproducir el seguimiento de producción.
- Si usa las versiones de producción y archivos de definición de seguimiento de rendimiento y el rendimiento seguimiento definición filtra los seguimientos "publicadas" para una base de datos de interés, análisis muestra que el **seguimiento del rendimiento** es de tamaño aproximadamente 15 veces mayor que el **producción seguimiento** tamaño.

## <a name="set-up-a-virtual-network-or-domain"></a>Configurar una red virtual o dominio

Reproducción distribuida, deberá usar cuentas comunes entre las máquinas. Debido a este requisito y por motivos de seguridad, se recomienda ejecutar Distributed Replay en una red virtual o en una red controlado por dominio:

- Crear el controlador y el cliente máquinas en el entorno.
- Asegúrese de que las máquinas de controlador y el cliente pueden hacer ping entre sí a través de la red.
- Equipos de cliente de reproducción distribuidos deben tener conectividad con el equipo de destino de reproducción que ejecuta SQL Server.

## <a name="set-up-the-controller-service"></a>Configurar el servicio de controlador

Para configurar el servicio del controlador:

1. Instale el controlador de Distributed Replay mediante el instalador de SQL Server. Si omite el paso del Asistente de instalador de SQL Server que configura el controlador de Distributed Replay, puede configurar el controlador a través del archivo de configuración. En una instalación típica, el archivo de configuración se encuentra en C:\Program Files (x86) \Microsoft SQL Server\<versión\>\Tools\DReplayController\DReplayController.config.
1. Los registros de controlador de reproducción distribuidos se encuentran en C:\Program Files (x86) \Microsoft SQL Server\<versión\>\Tools\DReplayController\Log.
1. Abra Services.msc y vaya a la **SQL Server Distributed Replay Controller** service.
1. Haga doble clic en el servicio y, a continuación, seleccione **propiedades**. Establecer la cuenta de servicio en una cuenta que es común a las máquinas de controlador y el cliente de la red.
1. Seleccione **Aceptar** para cerrar el **propiedades** ventana.
1. Reinicie el **SQL Server Distributed Replay Controller** desde Services.msc. También puede ejecutar los siguientes comandos en la línea de comandos para reiniciar el servicio:<br/>
   `NET STOP "SQL Server Distributed Replay Controller"`<br/>
   `NET START "SQL Server Distributed Replay Controller"`
1. Para obtener más opciones de configuración, consulte [configurar Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/configure-distributed-replay).

## <a name="configure-dcom"></a>Configurar DCOM

Esta configuración solo es necesario en la máquina del controlador.

1. Abra dcomcnfg.exe.
1. Expanda **servicios de componentes** > **equipos** > **mi equipo** > **configuración DCOM**.
1. En **configuración DCOM**, haga clic en **DReplayController**y, a continuación, seleccione **propiedades**.
1. Seleccione la pestaña **Seguridad** .
1. En **permisos de inicio y activación**, seleccione **personalizar**y, a continuación, seleccione **editar**.
1. Agregue el usuario que se iniciará la reproducción. Conceda al usuario los permisos ejecución Local y activación Local. Si el usuario tiene previsto ejecutar o activar de forma remota, conceda al usuario permisos de ejecución remota y activación remota.
1. Seleccione **Aceptar** para confirmar los cambios y volver a la **seguridad** ficha.
1. En **permisos de acceso**, seleccione **personalizar**y, a continuación, seleccione **editar**.
1. Agregue el usuario que se iniciará la reproducción. Conceda al usuario permisos de acceso Local. Si el usuario tiene previsto tener acceso al servicio de controlador de forma remota, conceda al usuario permisos de acceso remoto.
1. Seleccione **Aceptar** para confirmar los cambios y volver a la **seguridad** ficha.
1. Seleccione **Aceptar** para confirmar los cambios.
1. Reinicie el servicio de SQL Server Distributed Replay Controller desde Services.msc. También puede ejecutar los siguientes comandos en la línea de comandos para reiniciar el servicio:<br/>
   `NET STOP "SQL Server Distributed Replay Controller"`<br/>
   `NET START "SQL Server Distributed Replay Controller"`

## <a name="set-up-the-client-service"></a>Configurar el servicio de cliente

Antes de configurar el servicio de cliente, utilice las herramientas de red, como ping para comprobar que las máquinas de controlador y el cliente pueden comunicarse.

1. Instalar al cliente de Distributed Replay mediante el instalador de SQL Server.
1. Abra Services.msc y vaya al servicio de SQL Server Distributed Replay Client.
1. Haga doble clic en el servicio y, a continuación, seleccione **propiedades**. Establecer la cuenta de servicio en una cuenta que es común a las máquinas del controlador y el cliente de la red.
1. Seleccione **Aceptar** para cerrar el **propiedades** ventana. Si omite el paso del Asistente de instalador de SQL Server para configurar al cliente de Distributed Replay, puede configurarlo mediante el archivo de configuración. En una instalación típica, el archivo de configuración se encuentra en C:\Program Files (x86) \Microsoft SQL Server\<versión\>\Tools\DReplayClient\DReplayClient.config.
1. Asegúrese de que el archivo DReplayClient.config contiene el nombre de la máquina del controlador como su controlador para el registro.
1.  Reinicie el servicio de SQL Server Distributed Replay Client desde Services.msc. También puede ejecutar los siguientes comandos desde la línea de comandos para reiniciar el servicio:<br/>
    `NET STOP "SQL Server Distributed Replay Client"`<br/>
    `NET START "SQL Server Distributed Replay Client"`
1. Los registros de controlador de reproducción distribuidos se encuentran en C:\Program Files (x86) \Microsoft SQL Server\<versión\>\Tools\DReplayClient\Log. Los registros indican si el cliente se puede registrar con el controlador.
1. Si la configuración es correcta, el registro muestra el mensaje "registrado con el controlador < nombre del controlador\>".
1. Para obtener más opciones de configuración, consulte [configurar Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/configure-distributed-replay).

## <a name="set-up-distributed-replay-administration-tools"></a>Configurar las herramientas de administración de Distributed Replay

Puede usar herramientas de administración de Distributed Replay para probar rápidamente si Distributed Replay funciona correctamente en el entorno. Probando la configuración puede ser especialmente útil en un entorno en el que se registran varias máquinas de cliente con un controlador. Es posible que deba instalar SQL Server Management Studio (SSMS) para obtener las herramientas de administración.

1. Vaya a la de SSMS ubicación de instalación y busque la Distributed Replay administration herramienta dreplay.exe y sus componentes dependientes.
1. Abra una ventana del símbolo del sistema y ejecute `dreplay.exe status -f 1`.
1. Si todos los pasos anteriores se realizan correctamente, la salida de la consola indica que el controlador puede ver sus clientes en un `READY` estado.

## <a name="configure-the-firewall-for-remote-distributed-replay-access"></a>Configurar el firewall para el acceso remoto de Distributed Replay

Acceso remoto a Distributed Replay requiere la apertura de puertos que están visibles dentro del dominio o la red virtual.

1. Abra **Windows Firewall** con **seguridad avanzada**.
1. Vaya a **reglas de entrada**.
1. Crear una nueva regla de firewall de entrada para el programa C:\Program Files (x86) \Microsoft SQL Server\<versión\>\Tools\DReplayController\DReplayController.exe.
1. Permitir el acceso de nivel de dominio para todos los puertos para DReplayController.exe poder comunicarse con el servicio del controlador de forma remota.
1. Guardar la regla.

## <a name="set-up-target-computers"></a>Configurar los equipos de destino

Las dos reproducciones son necesarios para ejecutar una A o B prueba o un experimento. Es decir, dos instancias independientes de las instalaciones de SQL Server que necesite para un escenario de migración. 

También puede instalar las dos versiones de instancias de SQL Server en el mismo equipo. Es una advertencia para asegurarse de que las instancias se aíslan completamente cuando una reproducción en curso.

Los pasos siguientes deben realizarse para cada reproducción:

1. Restaure la copia de seguridad de la base de datos.
1. Proporcionar permisos para el usuario de cuenta de servicio de cliente tener acceso a las bases de datos en la instancia de SQL Server. Se requieren permisos para las consultas que se ejecuta en la instancia de SQL Server.
1. Iniciar la reproducción.

## <a name="next-steps"></a>Pasos siguientes

- Para obtener información sobre cómo reproducir un seguimiento capturado en un entorno de prueba actualizada, consulte [reproducir seguimiento](database-experimentation-assistant-replay-trace.md).

- Para obtener una introducción minutos 19 DEA y demostración, vea el vídeo siguiente:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
