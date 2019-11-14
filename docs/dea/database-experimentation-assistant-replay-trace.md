---
title: Reproducir un seguimiento para las actualizaciones de SQL Server
description: Reproducir un seguimiento con Asistente para experimentación con bases de datos para las actualizaciones de SQL Server
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
ms.openlocfilehash: b1607aefdc8495f374b2586b0b896f20e87f62d1
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056703"
---
# <a name="replay-a-trace-in-database-experimentation-assistant"></a>Reproducir un seguimiento en Asistente para experimentación con bases de datos

En Asistente para experimentación con bases de datos (DEA), puede reproducir un archivo de seguimiento capturado en un entorno de prueba actualizado. Por ejemplo, considere una carga de trabajo de producción que se ejecuta en SQL Server 2008 R2. El archivo de seguimiento de la carga de trabajo se debe reproducir dos veces: una vez en un entorno con la misma versión de SQL Server que se ejecuta en producción y de nuevo en un entorno que tiene el destino de actualización SQL Server versión, como SQL Server 2016.

> [!NOTE]
> Para ejecutar esta acción, debe configurar manualmente máquinas virtuales o máquinas físicas para ejecutar seguimientos de Distributed Replay. Para obtener más información, consulte [controlador de Distributed Replay y configuración de clientes](https://blogs.msdn.microsoft.com/datamigration/distributed-replay-controller-and-client-setup/).
>
>

## <a name="create-a-trace-replay"></a>Crear una reproducción de seguimiento

En DEA, seleccione el icono de menú. En el menú expandido, seleccione **reproducir seguimientos** junto al icono reproducir.

![Seleccione reproducir seguimientos en el menú](./media/database-experimentation-assistant-replay-trace/dea-replay-trace-open.png)

> [!NOTE]
> El equipo del controlador de Distributed Replay requiere permisos para la cuenta de usuario que usa para el acceso remoto.
>

### <a name="grant-access-to-the-distributed-replay-controller"></a>Conceder acceso al controlador de Distributed Replay

1. En un símbolo del sistema, escriba **dcomcnfg** para abrir la interfaz de **servicios de componentes** .
1. Expanda **servicios de componentes** > **equipos** > **mi PC** > **Configuración DCOM** > **DReplayController**.
1. Haga clic con el botón secundario en **DReplayController**y seleccione **propiedades**.
1. En la pestaña **seguridad** , seleccione **Editar** para agregar la cuenta de usuario.
1. Seleccione **Aceptar**.

### <a name="verify-setup"></a>Comprobar la configuración

1.  **SQL Server ruta de instalación**: escriba la ruta de acceso a la ubicación en la que está instalado SQL Server. Por ejemplo, C:\\archivos de programa (x86)\\Microsoft SQL Server\\120.
1.  **Nombre del equipo del controlador**: escriba un nombre para la máquina que se ha configurado como controlador. Este equipo está ejecutando el servicio de Windows denominado SQL Server controlador de Distributed Replay. El controlador de Distributed Replay organiza las acciones de los clientes de Distributed Replay. Solo puede haber una instancia de controlador en cada entorno de Distributed Replay.
1.  **Nombres de equipos cliente**: escriba un nombre para cada equipo cliente, separados por comas. Ejemplo: client1, cliente2. Puede tener hasta cinco controladores de cliente. Los clientes son uno o más equipos, ya sean físicos o virtuales, que ejecutan el servicio de Windows denominado SQL Server cliente de Distributed Replay. Los clientes de Distributed Replay colaboran para simular cargas de trabajo en una instancia de SQL Server. Puede haber uno o más clientes en cada entorno de Distributed Replay.
1.  Seleccione **Siguiente**.

### <a name="select-a-trace"></a>Seleccionar un seguimiento

1.  **Ruta de acceso al archivo de seguimiento**: escriba la ruta de acceso al archivo de seguimiento de entrada (. TRC).
1.  **Ruta de acceso para almacenar la salida de preprocesamiento de reproducción**:  
    \- si aún no tiene el archivo IRF, escriba la ruta de acceso a la ubicación donde desea almacenar el archivo IRF y otras salidas de preprocesamiento.  
    \- si ya tiene el archivo IRF, escriba la ruta de acceso a los archivos IRF.
1. Seleccione **Siguiente**.

### <a name="replay-a-trace"></a>Reproducir un seguimiento

1.  **Nombre del archivo de seguimiento**: escriba un nombre de archivo de seguimiento.
1.  **Tamaño máximo de archivo (MB)** : escriba un valor de tamaño de sustitución del archivo de seguimiento. El valor predeterminado es 200 MB. Puede especificar un valor personalizado.
1.  **Ruta de acceso para almacenar el resultado del seguimiento de reproducción**: escriba la ruta de acceso del archivo. TRC de salida.
1.  **Nombre**de la instancia de SQL Server: escriba el nombre de la instancia de SQL Server en la que se van a reproducir los seguimientos.
1.  Seleccione **Inicio**.

Si la información introducida es válida, se inicia el proceso de Distributed Replay. De lo contrario, el texto boses que tiene información incorrecta se resalta con rojo. Asegúrese de que los valores especificados son correctos y, a continuación, seleccione **iniciar**.

Espere hasta que finalice la reproducción para ver la ubicación que especificó. Seleccione el icono de campana en la parte inferior del menú de la izquierda para supervisar el progreso de la reproducción.

![Progreso de la reproducción de seguimientos](./media/database-experimentation-assistant-replay-trace/dea-replay-trace-progress.png)

## <a name="frequently-asked-questions-about-trace-replay"></a>Preguntas más frecuentes sobre la reproducción de seguimiento

### <a name="what-security-permissions-do-i-need-to-start-a-replay-capture-on-my-target-server"></a>¿Qué permisos de seguridad necesito para iniciar una captura de reproducción en el servidor de destino?

- El usuario de Windows que ejecuta la operación de seguimiento en la aplicación de DEA debe tener derechos de administrador del sistema en el equipo de destino que ejecuta SQL Server. Estos derechos de usuario son necesarios para iniciar un seguimiento.
- La cuenta de servicio en la que se ejecuta el equipo de destino que ejecuta SQL Server debe tener acceso de escritura a la ruta de acceso del archivo de seguimiento especificada.
- La cuenta de servicio en la que se ejecutan los servicios de cliente de Distributed Replay debe tener derechos de usuario para conectarse al equipo de destino que ejecuta SQL Server y ejecutar consultas.

### <a name="can-i-start-more-than-one-replay-in-the-same-session"></a>¿Puedo iniciar más de una reproducción en la misma sesión?

Sí, puede iniciar varias reproducciones y realizar un seguimiento de ellas hasta su finalización en la misma sesión.

### <a name="can-i-start-more-than-one-replay-in-parallel"></a>¿Se puede iniciar más de una reproducción en paralelo?

Sí, pero no con el mismo conjunto de equipos seleccionados en **controlador más clientes**. El controlador y los clientes estarán ocupados. Configure un conjunto independiente de equipos en **controlador más cliente** para iniciar una reproducción paralela.

### <a name="how-long-does-a-replay-typically-take-to-finish"></a>¿Cuánto tiempo tarda una reproducción en finalizar?

Una reproducción suele tardar la misma cantidad de tiempo que el seguimiento de origen más la cantidad de tiempo que se tarda en preprocesar el seguimiento de origen. Sin embargo, si los equipos cliente que están registrados con el controlador no son suficientes para administrar la carga que se produce a partir de la reproducción, la reproducción puede tardar más tiempo en completarse. Puede registrar hasta 16 máquinas cliente con el controlador.

### <a name="how-large-do-target-trace-files-get"></a>¿Cómo se obtienen los archivos de seguimiento de destino de gran tamaño?

Los archivos de seguimiento de destino pueden estar entre 5 y 15 veces el tamaño del seguimiento de origen. El tamaño del archivo se basa en el número de consultas que se ejecutan. Por ejemplo, los blobs del plan de consulta pueden ser grandes. Si las estadísticas de estas consultas cambian con frecuencia, se capturan más eventos.

### <a name="why-do-i-need-to-restore-databases"></a>¿Por qué es necesario restaurar las bases de datos?

SQL Server es un sistema de administración de bases de datos relacionales con estado. Para ejecutar correctamente una prueba A/B, el estado de la base de datos se debe conservar en todo momento. De lo contrario, es posible que vea errores en las consultas durante la reproducción que no aparecerán en producción. Para evitar estos errores, se recomienda que realice una copia de seguridad justo antes de la captura de origen. Del mismo modo, es necesario restaurar la copia de seguridad en el equipo de destino que ejecuta SQL Server para evitar errores durante la reproducción.

### <a name="what-does-pass--on-the-replay-page-mean"></a>¿Qué significa "pass%" en la página de reproducción?

El **paso%** significa que solo se pasó un porcentaje de consultas. Puede diagnosticar si se espera el número de errores. Es posible que se produzcan errores o que se produzcan errores porque la base de datos ha perdido su integridad. Si el valor de **Pass%** no es el esperado, puede detener el seguimiento y ver el archivo de seguimiento en SQL Profiler para ver qué consultas no se han realizado correctamente.

### <a name="how-can-i-look-at-the-trace-events-that-were-collected-during-replay"></a>¿Cómo puedo ver los eventos de seguimiento recopilados durante la reproducción?

Abra un archivo de seguimiento de destino y verlo en SQL Server Profiler. O bien, si desea realizar modificaciones en la captura de reproducción, todos los scripts de SQL Server están disponibles en C:\\Program Files (x86)\\Microsoft Corporation\\Asistente para experimentación con bases de datos\\scripts\\StartReplayCapture. SQL.

### <a name="what-trace-events-does-dea-collect-during-replay"></a>¿Qué eventos de seguimiento recopilan DEA durante la reproducción?

DEA captura eventos de seguimiento que contienen información relacionada con el rendimiento. La configuración de captura está en el script StartReplayCaptureTrace. SQL. Estos eventos son típicos SQL Server eventos de seguimiento que se enumeran en la [documentación de referencia de sp_trace_setevent (Transact-SQL)](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql).

## <a name="troubleshoot-trace-replay"></a>Solucionar problemas de reproducción de seguimiento

### <a name="i-cant-connect-to-the-computer-thats-running-sql-server"></a>No puedo conectarme al equipo que ejecuta SQL Server

- Confirme que el nombre del equipo que ejecuta SQL Server es válido. Para confirmar, intente conectarse al servidor mediante SQL Server Management Studio (SSMS).
- Confirme que la configuración del firewall no bloquea las conexiones con el equipo que ejecuta SQL Server.
- Confirme que el usuario tiene los derechos de usuario necesarios.
- Confirme que la cuenta de servicio del cliente de Distributed Replay tiene acceso al equipo que ejecuta SQL Server.

Puede obtener más detalles en los registros en% Temp%\\DEA. Si el problema persiste, póngase en contacto con el equipo del producto.

### <a name="i-cant-connect-to-the-distributed-replay-controller"></a>No puedo conectarme al controlador de Distributed Replay

- Compruebe que el servicio del controlador de Distributed Replay se está ejecutando en el equipo del controlador. Para comprobarlo, use las herramientas de administración de Distributed Replay (ejecute el comando `dreplay.exe status -f 1`).
- Si la reproducción se inicia de forma remota:
  - Confirme que el equipo que ejecuta DEA puede hacer ping correctamente en el controlador. Confirme que la configuración del Firewall permite conexiones según las instrucciones de la página **configurar el entorno de reproducción** . Para obtener más información, vea el artículo [SQL Server Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/sql-server-distributed-replay?view=sql-server-2017).
  - Asegúrese de que se permite el inicio remoto DCOM y la activación remota para el usuario del controlador de Distributed Replay.
  - Asegúrese de que los derechos de usuario de acceso remoto DCOM están permitidos para el usuario del controlador de Distributed Replay.

### <a name="the-trace-file-path-exists-on-my-machine-why-cant-distributed-replay-controller-find-it"></a>La ruta de acceso del archivo de seguimiento existe en mi máquina. ¿Por qué no se encuentra Distributed Replay controlador?

Distributed Replay solo puede tener acceso a los recursos del disco local. Debe copiar los archivos de seguimiento de origen en la máquina del controlador de Distributed Replay antes de iniciar la reproducción. Además, debe proporcionar la ruta de acceso en la página de **nueva reproducción** de DEA. 

Las rutas UNC no son compatibles con Distributed Replay. Distributed Replay rutas de acceso deben ser rutas de acceso absolutas y locales al primer archivo de seguimiento de origen, incluida la extensión.

### <a name="why-cant-i-browse-for-files-on-the-new-replay-page"></a>¿Por qué no se pueden buscar archivos en la nueva página de reproducción?

Dado que no se pueden examinar las carpetas de un equipo remoto, la exploración de archivos no es útil. Copiar y pegar las rutas de acceso absolutas es más eficaz.

### <a name="i-started-replay-with-a-trace-but-distributed-replay-didnt-replay-any-events"></a>He iniciado la reproducción con un seguimiento pero Distributed Replay no ha reproducido ningún evento

Este problema puede deberse a que el archivo de seguimiento no tiene eventos reproducibles o a que no tiene información sobre cómo reproducir eventos. Confirme si la ruta de acceso al archivo de seguimiento proporcionada es un archivo de seguimiento de origen. El archivo de seguimiento de origen se crea con la configuración proporcionada en el script StartCaptureTrace. SQL.

### <a name="i-see-unexpected-error-occurred-when-i-try-to-preprocess-my-trace-files-by-using-the-sql-server-2017-distributed-replay-controller"></a>Aparece el mensaje "error inesperado" al intentar preprocesar los archivos de seguimiento mediante el controlador SQL Server 2017 Distributed Replay

Este problema se conoce en la versión RTM de SQL Server 2017. Para obtener más información, vea [error inesperado al usar la característica de DReplay para reproducir un seguimiento capturado en SQL Server 2017](https://support.microsoft.com/help/4045678/fix-unexpected-error-when-you-use-the-dreplay-feature-to-replay-a).  
  
El problema se ha solucionado en la última actualización acumulativa 1 de SQL Server 2017. Descargue la versión más reciente de la [actualización acumulativa 1 para SQL Server 2017](https://support.microsoft.com/help/4038634/cumulative-update-1-for-sql-server-2017).

## <a name="next-steps"></a>Pasos siguientes

- Para crear un informe de análisis que le ayude a obtener información sobre los cambios propuestos, vea [crear informes](database-experimentation-assistant-create-report.md).

- Para obtener una introducción de 19 minutos a DEA y demostraciones, vea el siguiente vídeo:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
