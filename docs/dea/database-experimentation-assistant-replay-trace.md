---
title: Reproducir un seguimiento con el Asistente para experimentación de base de datos para las actualizaciones de SQL Server
description: Reproducir un seguimiento con el Asistente para experimentación de base de datos
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
ms.openlocfilehash: 09c3ffe6897107d2b3db0f53b0fdc895ee437efd
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2018
ms.locfileid: "56987711"
---
# <a name="replay-a-trace-in-database-experimentation-assistant"></a>Reproducir un seguimiento en el Asistente de experimentación de base de datos

En base de datos experimentación Assistant (DEA), puede reproducir un archivo de seguimiento capturado contra un entorno de pruebas actualizado. Por ejemplo, considere la posibilidad de una carga de trabajo de producción que se ejecuta en SQL Server 2008 R2. El archivo de seguimiento para la carga de trabajo debe reproducirse dos veces: una vez en un entorno con la misma versión de SQL Server que se ejecuta en producción y otra vez en un entorno que tiene la versión de SQL Server de destino para la actualización, como SQL Server 2016.

> [!NOTE]
> Para ejecutar esta acción, debe establecer manualmente las máquinas virtuales o máquinas físicas para ejecutar Distributed Replay seguimientos. Para obtener más información, consulte [el programa de instalación de controlador y los clientes de Distributed Replay](https://blogs.msdn.microsoft.com/datamigration/distributed-replay-controller-and-client-setup/).
>
>

## <a name="create-a-trace-replay"></a>Crear una reproducción de seguimiento

En DEA, seleccione el icono de menú. En el menú expandido, seleccione **reproducir seguimientos** junto al icono de reproducción.

![Seleccione reproducir seguimientos en el menú](./media/database-experimentation-assistant-replay-trace/dea-replay-trace-open.png)

> [!NOTE]
> La máquina del controlador de Distributed Replay requiere permisos a la cuenta de usuario que usa para remoto.
>

### <a name="grant-access-to-the-distributed-replay-controller"></a>Conceder acceso al controlador de Distributed Replay

1. En un símbolo del sistema, escriba **dcomcnfg** para abrir el **servicios de componentes** interfaz.
1. Expanda **servicios de componentes** > **equipos** > **mi equipo** > **configuración DCOM**  >  **DReplayController**.
1. Haga clic en **DReplayController**y, a continuación, seleccione **propiedades**.
1. En el **seguridad** ficha, seleccione **editar** para agregar la cuenta de usuario.
1. Seleccione **Aceptar**.

### <a name="verify-setup"></a>Compruebe que el programa de instalación

1.  **Ruta de instalación de SQL Server**: Escriba la ruta de acceso donde está instalado SQL Server. Por ejemplo, C:\\archivos de programa (x86)\\Microsoft SQL Server\\120.
1.  **Nombre del equipo controlador**: Escriba un nombre para la máquina que se ha establecido como el controlador. Esta máquina se está ejecutando el servicio de Windows denominado controlador de SQL Server Distributed Replay. El controlador de Distributed Replay orquestra las acciones de los clientes de Distributed Replay. Solo puede haber una instancia de controlador en cada entorno de Distributed Replay.
1.  **Los nombres de equipo cliente**: Escriba un nombre para cada equipo cliente, separado por comas. Ejemplo: client1, client2. Puede tener hasta cinco de los controladores de cliente. Los clientes son uno o varios equipos, ya sea físicos o virtuales, que ejecutan el servicio de Windows denominado a cliente de SQL Server Distributed Replay. Los clientes de Distributed Replay colaboran para simular cargas de trabajo en una instancia de SQL Server. Puede haber uno o más clientes en cada entorno de Distributed Replay.
1.  Seleccione **Siguiente**.

### <a name="select-a-trace"></a>Seleccione un seguimiento

1.  **Ruta de acceso al archivo de seguimiento**: Escriba la ruta de acceso al archivo de entrada de seguimiento (.trc).
1.  **Ruta de acceso para almacenar la reproducción de preprocesamiento salida**:  
    \- Si aún no tiene el archivo IRF, escriba la ruta de acceso a la ubicación donde desea almacenar el archivo IRF y genera otro preprocesamiento.  
    \- Si ya tiene el archivo IRF, escriba la ruta de acceso a los archivos IRF.
1. Seleccione **Siguiente**.

### <a name="replay-a-trace"></a>Reproducir un seguimiento

1.  **Nombre de archivo de seguimiento**: Escriba un nombre de archivo de seguimiento.
1.  **Tamaño máximo de archivo (MB)**: Escriba un valor de tamaño de sustitución incremental de archivo de seguimiento. El valor predeterminado es 200 MB. Puede especificar un valor personalizado.
1.  **Ruta de acceso para almacenar el resultado del seguimiento de reproducción**: Escriba la ruta de acceso del archivo de salida. trc.
1.  **Nombre de instancia de SQL Server**:  Escriba el nombre de la instancia de SQL Server en el que se va a reproducir seguimientos.
1.  Seleccione **Inicio**.

Si la información que escribió es válida, se inicia el proceso de Distributed Replay. En caso contrario, se resaltan el boses de texto que tiene información incorrecta con color rojo. Asegúrese de que los valores especificados son correctos y, a continuación, seleccione **iniciar**.

Espere a que termine la reproducción de ejecución para ver la ubicación que especificó. Seleccione el icono de campana en la parte inferior del menú izquierdo para supervisar el progreso de la reproducción.

![Progreso de los seguimientos de reproducción](./media/database-experimentation-assistant-replay-trace/dea-replay-trace-progress.png)

## <a name="frequently-asked-questions-about-trace-replay"></a>Preguntas más frecuentes acerca de la reproducción de seguimiento

### <a name="what-security-permissions-do-i-need-to-start-a-replay-capture-on-my-target-server"></a>¿Qué permisos de seguridad es necesario iniciar una captura de reproducción en el servidor de destino?

- El usuario de Windows que se ejecuta la operación de seguimiento en la aplicación DEA debe tener derechos de sysadmin en el equipo de destino que ejecuta SQL Server. Estos derechos de usuario son necesarios para iniciar un seguimiento.
- La cuenta de servicio en la que se está ejecutando el equipo de destino que ejecuta SQL Server debe tener acceso de escritura a la ruta de acceso del archivo de seguimiento especificado.
- La cuenta de servicio en la que se ejecutan los servicios de Distributed Replay Client debe tener derechos de usuario para conectarse al equipo de destino que ejecuta SQL Server y ejecutar consultas.

### <a name="can-i-start-more-than-one-replay-in-the-same-session"></a>¿Se puede iniciar más de una reproducción en la misma sesión?

Sí, puede iniciar varias reproducciones y realizar un seguimiento de ellos hasta su finalización en la misma sesión.

### <a name="can-i-start-more-than-one-replay-in-parallel"></a>¿Se puede iniciar más de una reproducción en paralelo?

Sí, pero no con el mismo conjunto de máquinas seleccionadas en **controlador además de los clientes**. El controlador y los clientes será ocupados. Configurar un conjunto independiente de las máquinas en **controlador más cliente** para iniciar una reproducción en paralelo.

### <a name="how-long-does-a-replay-typically-take-to-finish"></a>¿Cuánto una reproducción normalmente tarda en Finalizar?

Una reproducción toma normalmente la misma cantidad de tiempo que el seguimiento de origen más la cantidad de tiempo necesario para preprocesar el seguimiento de origen. Sin embargo, si los equipos cliente que están registrados con el controlador no están suficientes para administrar la carga que se genera desde la reproducción, la reproducción puede tardar más tiempo en completarse. Puede registrar hasta 16 máquinas de cliente con el controlador.

### <a name="how-large-do-target-trace-files-get"></a>¿Tamaño logramos los archivos de seguimiento de destino?

El seguimiento de destino podrían ser archivos entre 5 y 15 veces el tamaño de la traza de origen. El tamaño del archivo se basa en el número de consultas se ejecuta. Por ejemplo, los blobs del plan de consulta pueden ser grandes. Si las estadísticas de estas consultas se cambian a menudo, se capturan más eventos.

### <a name="why-do-i-need-to-restore-databases"></a>¿Por qué es necesario restaurar las bases de datos?

SQL Server es un sistema de administración de base de datos relacional con estado. Para ejecutar correctamente una A / B prueba, el estado de la base de datos debe conservarse en todo momento. En caso contrario, pueden aparecer errores en las consultas durante la reproducción que no aparece en producción. Para evitar estos errores, recomendamos que realice una copia de seguridad justo antes de la captura de origen. De forma similar, restaurar la copia de seguridad del equipo de destino que ejecuta SQL Server es necesario para evitar errores durante la reproducción.

### <a name="what-does-pass--on-the-replay-page-mean"></a>¿Qué "pass %" en la media de la página de reproducción?

**Pasar %** significa que solo un porcentaje de consultas pasa. Puede diagnosticar si se espera que el número de errores. Los errores que podrían esperarse, o los errores podrían producirse porque la base de datos ha perdido su integridad. Si el valor de **pass %** no es de esperar, puede detener el seguimiento y examine el archivo de seguimiento en SQL Profiler para ver las consultas que no se realizó correctamente.

### <a name="how-can-i-look-at-the-trace-events-that-were-collected-during-replay"></a>¿Cómo puedo buscar en los eventos de seguimiento que se recopilaron durante la reproducción

Abra un archivo de seguimiento de destino y verlo en SQL Profiler. O bien, si desea realizar modificaciones en la captura de reproducción, todos los scripts de SQL Server están disponibles en C:\\archivos de programa (x86)\\Microsoft Corporation\\Ayudante de experimentación de base de datos\\lassecuenciasdecomandos\\ StartReplayCapture.sql.

### <a name="what-trace-events-does-dea-collect-during-replay"></a>¿Qué eventos de seguimiento recopila DEA durante la reproducción?

DEA captura los eventos de seguimiento que contienen información relacionada con el rendimiento. La configuración de captura está en la secuencia de comandos StartReplayCaptureTrace.sql. Estos eventos son eventos de seguimiento de SQL Server típicos que se muestran en el [documentación de referencia sp_trace_setevent (Transact-SQL)](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql).

## <a name="troubleshoot-trace-replay"></a>Solución de problemas de reproducción de seguimiento

### <a name="i-cant-connect-to-the-computer-thats-running-sql-server"></a>No puedo conectarme al equipo que ejecuta SQL Server

- Confirme que el nombre del equipo que ejecuta SQL Server es válido. Para confirmar, intente conectarse al servidor mediante el uso de SQL Server Management Studio (SSMS).
- Confirme que la configuración del firewall no bloquea las conexiones con el equipo que ejecuta SQL Server.
- Confirme que el usuario tiene los derechos de usuario necesarios.
- Confirme que la cuenta de servicio del cliente de Distributed Replay tiene acceso al equipo que ejecuta SQL Server.

Puede obtener más detalles en los registros en % temp %\\DEA. Si el problema persiste, póngase en contacto con el equipo del producto.

### <a name="i-cant-connect-to-the-distributed-replay-controller"></a>No puedo conectarme al controlador de Distributed Replay

- Compruebe que el servicio Distributed Replay controller se está ejecutando en la máquina del controlador. Para comprobar, use las herramientas de administración de Distributed Replay (ejecute el comando `dreplay.exe status -f 1`).
- Si la reproducción se inicia de forma remota:
  - Confirme que la máquina que ejecuta DEA hacer ping correctamente en el controlador. Confirme que la configuración de firewall permite las conexiones según las instrucciones en el **configurar el entorno de reproducción** página. Para obtener más información, vea el artículo [SQL Server Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/sql-server-distributed-replay?view=sql-server-2017).
  - Asegúrese de que se permiten la ejecución remota de DCOM y activación remota para el usuario de Distributed Replay controller.
  - Asegúrese de que se permiten los derechos de usuario de acceso remoto de DCOM para el usuario del controlador de Distributed Replay.

### <a name="the-trace-file-path-exists-on-my-machine-why-cant-distributed-replay-controller-find-it"></a>La ruta de acceso del archivo de seguimiento existe en mi equipo. ¿Por qué no encuentra el controlador de Distributed Replay?

Reproducción distribuida puede tener acceso a únicamente los recursos de disco local. Debe copiar los archivos de seguimiento de origen a la máquina del controlador de Distributed Replay antes de iniciar la reproducción. Además, debe proporcionar la ruta de acceso en la DEA **reproducción nuevo** página. 

Rutas de acceso UNC no son compatibles con Distributed Replay. Las rutas de acceso de reproducción distribuidas deben ser locales rutas de acceso absolutas para el primer archivo de seguimiento de origen, incluida la extensión.

### <a name="why-cant-i-browse-for-files-on-the-new-replay-page"></a>¿Por qué no puedo examinar archivos en la página de reproducción nuevo?

Dado que no podemos examinar las carpetas de un equipo remoto, exploración de archivos no es útil. Copiar y pegar las rutas de acceso absolutas es más eficaz.

### <a name="i-started-replay-with-a-trace-but-distributed-replay-didnt-replay-any-events"></a>Comencé a trabajar reproducción con un seguimiento pero Distributed Replay no reproducir los eventos

Este problema puede producirse porque el archivo de seguimiento no tiene eventos reproducibles o no tiene información acerca de cómo reproducir los eventos. Confirme si la ruta de archivo de seguimiento proporcionada es un archivo de seguimiento de origen. El archivo de origen de seguimiento se crea mediante la configuración proporcionada en el script StartCaptureTrace.sql.

### <a name="i-see-unexpected-error-occurred-when-i-try-to-preprocess-my-trace-files-by-using-the-sql-server-2017-distributed-replay-controller"></a>Consulte la "error inesperado occurred!" Cuando intento preprocesar los archivos de seguimiento mediante el uso de SQL Server 2017 Distributed Replay controller

Este problema se conoce en la versión RTM de SQL Server 2017. Para obtener más información, consulte [error inesperado al usar la característica de DReplay para reproducir un seguimiento capturado de SQL Server 2017](https://support.microsoft.com/help/4045678/fix-unexpected-error-when-you-use-the-dreplay-feature-to-replay-a).  
  
El problema se ha corregido en la última actualización acumulativa 1 para SQL Server 2017. Descargue la versión más reciente de [actualización acumulativa 1 para SQL Server 2017](https://support.microsoft.com/help/4038634/cumulative-update-1-for-sql-server-2017).

## <a name="next-steps"></a>Pasos siguientes

- Para crear un informe de análisis que ayuda a obtener información detallada sobre los cambios propuestos, consulte [crear informes](database-experimentation-assistant-create-report.md).

- Para obtener una introducción minutos 19 DEA y demostración, vea el vídeo siguiente:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
