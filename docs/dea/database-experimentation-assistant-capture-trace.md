---
title: Capturar un seguimiento en Asistente para experimentación con bases de datos para las actualizaciones de SQL Server
description: Capturar un seguimiento en Asistente para experimentación con bases de datos
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
ms.reviewer: mathoma
ms.openlocfilehash: 3887daff7807d57244449d4f35d220bb47b8f10d
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653813"
---
# <a name="capture-a-trace-in-database-experimentation-assistant"></a>Capturar un seguimiento en Asistente para experimentación con bases de datos

Puede usar una captura de seguimiento en Asistente para experimentación con bases de datos (DEA) para crear un archivo de seguimiento que tenga un registro de eventos de servidor capturados. Un evento de servidor capturado es un evento que se produce en un servidor específico durante un período de tiempo específico. Una captura de seguimiento debe ejecutarse una vez por cada servidor.

Antes de iniciar una captura de seguimiento, asegúrese de hacer una copia de seguridad de todas las bases de datos de destino.

El almacenamiento en caché de consultas en SQL Server puede afectar a los resultados de la evaluación. Se recomienda reiniciar el servicio de SQL Server (MSSQLSERVER) en la aplicación de servicios para mejorar la coherencia de los resultados de la evaluación.

## <a name="create-a-trace-capture"></a>Crear una captura de seguimiento

1. En DEA, seleccione el icono de menú en el menú de la izquierda. En el menú expandido, seleccione **capturar seguimientos** junto al icono de la cámara.

    ![Seleccione capturar seguimientos en el menú](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-capture.png)

1. En **nueva captura**, escriba o seleccione la siguiente información:

    - **Nombre**de la instancia de SQL Server: Escriba un nombre para el equipo que ejecuta SQL Server en el que desea capturar un seguimiento de servidor.
    - **Nombre**de la base de datos: Escriba un nombre para la base de datos en la que se va a iniciar un seguimiento de base de datos. Si no se especifica una base de datos, el seguimiento se captura en todas las bases de datos del servidor.
    - **Nombre del archivo de seguimiento**: Escriba un nombre para el archivo de seguimiento de la captura.
    - **Tamaño máximo de archivo (MB)** : Seleccione el tamaño de sustitución de los archivos. Se creará un archivo nuevo según sea necesario en el tamaño de archivo que seleccione. El tamaño de sustitución recomendado es 200 MB.
    - **Duración (en minutos)** : Seleccione el período de tiempo (en minutos) durante el que desea que se ejecute la captura de seguimiento.
    - **Ruta de acceso para almacenar el archivo de seguimiento de salida**: Seleccione la ruta de acceso de destino del archivo de seguimiento. 

    > [!NOTE]
    > La ruta de acceso al archivo de seguimiento debe estar en el equipo que ejecuta SQL Server. Si el servicio SQL Server no está establecido para una cuenta específica, es posible que el servicio necesite permisos de escritura en la carpeta especificada para que se escriba el archivo de seguimiento.
    >
    >

    ![Nueva página de captura](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-inputs.png)

## <a name="start-the-trace-capture"></a>Iniciar la captura de seguimiento

Después de escribir o seleccionar la información necesaria, seleccione **iniciar** para iniciar la captura de seguimientos. Si la información introducida es válida, comienza el proceso de captura de seguimiento. De lo contrario, los cuadros de texto que tienen entradas no válidas se resaltan en rojo. 

Asegúrese de que los valores que ha seleccionado o especificado son correctos y, a continuación, seleccione **iniciar**.

Cuando termine de ejecutarse la captura de seguimiento, busque el nuevo archivo de seguimiento en la ubicación del archivo que especificó en **ruta de acceso para almacenar el archivo de seguimiento de salida**. Seleccione el icono de campana en la parte inferior del menú de la izquierda para supervisar el progreso de la captura.

![Progreso de la captura de seguimiento](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-progress.png)

### <a name="trace-file"></a>Archivo de seguimiento

La captura de seguimiento escribe un archivo. TRC en la ubicación especificada. El archivo de seguimiento incluye los resultados de seguimiento de la actividad de una base de datos de SQL Server. Los archivos TRC están diseñados para proporcionar más información acerca de los errores detectados e indicados por SQL Server.

## <a name="frequently-asked-questions-about-trace-capture"></a>Preguntas más frecuentes sobre la captura de seguimiento

A continuación se muestran algunas de las preguntas más frecuentes sobre la captura de seguimiento en DEA.

### <a name="what-events-are-captured-when-i-run-a-trace-capture-on-a-production-database"></a>¿Qué eventos se capturan cuando ejecuto una captura de seguimiento en una base de datos de producción?

En la tabla siguiente se proporciona la lista de eventos y los datos de columna correspondientes que se recopilan para los seguimientos:
  
|Nombre del evento|Datos de texto (1)|Datos binarios (2)|IDENTIFICADOR de base de datos (3)|Nombre de host (8)|Nombre de la aplicación (10)|Nombre de inicio de sesión (11)|SPID (12)|Hora de inicio (14)|Hora de finalización (15)|Nombre de la base de datos (35)|Secuencia de eventos (51)|IsSystem (60)|  
|---|---|---|---|---|---|---|---|---|---|---|---|---|  
|**RPC: completado (10)**||*|*|*|*|*|*|*|*|*|*|*|  
|**RPC: iniciando (11)**||*|*|*|*|*|*|*||*|*|*|  
|**Parámetro de salida RPC (100)**|*||*|*|*|*|*|*||*|*|*|  
|**SQL: BatchCompleted (12)**|*||*|*|*|*|*|*|*|*|*|*|  
|**SQL:BatchStarting (13)**|*||*|*|*|*|*|*||*|*|*|  
|**Auditar inicio de sesión (14)**|*|*|*|*|*|*|*|*||*|*|*|  
|**Fin de sesión de auditoría (15)**|*||*|*|*|*|*|*|*|*|*|*|  
|**ExistingConnection (17)**|*|*|*|*|*|*|*|*||*|*|*|  
|**CursorOpen (53)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorPrepare (70)**|*||*|*|*|*|*|*||*|*|*|  
|**Preparar SQL (71)**|||*|*|*|*|*|*||*|*|*|  
|**Exec Prepared SQL (72)**|||*|*|*|*|*|*||*|*|*|  
|**CursorExecute (74)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorUnprepare (77)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorClose (78)**|*||*|*|*|*|*|*||*|*|*|  

### <a name="is-there-a-performance-effect-on-my-production-server-when-trace-capture-is-running"></a>¿Hay algún efecto de rendimiento en el servidor de producción cuando se está ejecutando la captura de seguimiento?
    
Sí, hay un efecto mínimo en el rendimiento durante la recopilación de seguimiento. En nuestras pruebas, encontramos aproximadamente una presión de memoria del 3%.
    
### <a name="what-kind-of-permissions-are-required-for-capturing-traces-on-a-production-workload"></a>¿Qué tipo de permisos son necesarios para capturar seguimientos en una carga de trabajo de producción?
    
- El usuario de Windows que ejecuta la operación de seguimiento en la aplicación de DEA debe tener derechos de administrador del sistema en el equipo que ejecuta SQL Server.
- La cuenta de servicio usada en el equipo que ejecuta SQL Server debe tener acceso de escritura a la ruta de acceso del archivo de seguimiento especificada.

### <a name="can-i-capture-traces-for-the-entire-server-or-only-on-a-single-database"></a>¿Puedo capturar seguimientos para todo el servidor o solo en una base de datos única?
    
Puede usar DEA para capturar seguimientos para todas las bases de datos del servidor o para una sola base de datos.
    
### <a name="i-have-a-linked-server-configured-in-my-production-environment-do-those-queries-show-up-in-the-traces"></a>Tengo un servidor vinculado configurado en el entorno de producción. ¿Las consultas se muestran en los seguimientos?
    
Si está ejecutando una captura de seguimiento para todo el servidor, el seguimiento captura todas las consultas, incluidas las consultas de servidor vinculado. Para ejecutar una captura de seguimiento para todo el servidor, deje el cuadro Nombre de la **base de datos** en **nueva captura** vacía.
    
### <a name="whats-the-minimum-recommended-time-for-production-workload-traces"></a>¿Cuál es el tiempo mínimo recomendado para los seguimientos de carga de trabajo de producción?
    
Se recomienda elegir la hora que mejor represente la totalidad de la carga de trabajo. De este modo, el análisis se ejecuta en todas las consultas de la carga de trabajo.
    
### <a name="how-important-is-to-take-a-database-backup-right-before-i-start-a-trace-capture"></a>¿Es importante tomar una copia de seguridad de base de datos antes de iniciar una captura de seguimiento?
    
Antes de iniciar una captura de seguimiento, asegúrese de hacer una copia de seguridad de todas las bases de datos de destino. Se reproduce el seguimiento capturado en destino 1 y destino 2. Si el estado de la base de datos no es el mismo, se sesgan los resultados de la experimentación.

### <a name="can-i-collect-xevents-instead-of-traces-and-can-i-replay-xevents"></a>¿Puedo recopilar XEvents en lugar de seguimientos y puedo reproducir XEvents?
    
Sí. DEA es compatible con XEvents. Descargue la versión más reciente de DEA y pruébela.

## <a name="troubleshoot-trace-captures"></a>Solucionar problemas de capturas de seguimiento

Si ve un error al ejecutar una captura de seguimiento, revise los siguientes requisitos previos:

- Confirme que el nombre del equipo que ejecuta SQL Server es válido. Para confirmar, intente conectarse al equipo que ejecuta SQL Server mediante SQL Server Management Studio (SSMS).
- Confirme que la configuración del firewall no bloquea las conexiones con el equipo que ejecuta SQL Server.
- Confirme que el usuario tiene los permisos que se enumeran en las [preguntas más frecuentes sobre la reproducción](https://blogs.msdn.microsoft.com/datamigration/2017/03/24/dea-2-0-replay-faq/)de publicaciones de blog.
- Confirme que el nombre de seguimiento no sigue la Convención estándar de sustitución\_incremental (Capture 1). En su lugar, pruebe nombres de seguimiento\_como Capture 1A o Capture1.

A continuación se muestran algunos posibles errores que podrían aparecer y soluciones para resolverlos:

|Posibles errores|Solución|  
|---|---|  
|No se puede iniciar el seguimiento en el SQL Server de destino, compruebe si tiene los permisos necesarios y si la cuenta de SQL Server tiene acceso de escritura a la ruta del archivo de seguimiento especificada código de error de SQL (53)|El usuario que ejecuta la herramienta DEA debe tener acceso al equipo que ejecuta SQL Server. El usuario debe tener asignado el rol sysadmin.|  
|No se puede iniciar el seguimiento en el SQL Server de destino, compruebe si tiene los permisos necesarios y si la cuenta de SQL Server tiene acceso de escritura a la ruta del archivo de seguimiento especificada código de error de SQL (19062)|Es posible que la ruta de acceso especificada no exista o que la carpeta no tenga permisos de escritura para la cuenta en la que se están ejecutando los servicios de SQL Server (por ejemplo, servicio de red). La ruta de acceso debe existir y debe tener los permisos necesarios para que se inicie el seguimiento.|  
|Actualmente se está ejecutando un seguimiento de DEA en el servidor de destino.|Ya se está ejecutando un seguimiento activo en el servidor de destino. No se puede iniciar un nuevo seguimiento cuando un seguimiento de todo el servidor ya se está ejecutando.|  
|No se puede abrir la base de datos solicitada para capturar el seguimiento. Este error puede deberse a un nombre de base de datos incorrecto.|La base de datos especificada no existe o no es accesible para el usuario actual. Use el nombre de base de datos correcto.|  

Si ve algún otro error con la etiqueta *código de error de SQL*, consulte [motor de base de datos errores](https://docs.microsoft.com/sql/relational-databases/errors-events/database-engine-events-and-errors) para obtener descripciones detalladas.

## <a name="next-steps"></a>Pasos siguientes

- Para obtener información sobre cómo configurar las herramientas de Distributed Replay en SQL Server antes de reproducir un seguimiento capturado, consulte [configurar la reproducción](database-experimentation-assistant-configure-replay.md).

- Para obtener una introducción de 19 minutos a DEA y demostraciones, vea el siguiente vídeo:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
