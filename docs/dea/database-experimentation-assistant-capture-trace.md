---
title: Capture un seguimiento en el Asistente de experimentación de base de datos para las actualizaciones de SQL Server
description: Capture un seguimiento en el Asistente de experimentación de base de datos
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
ms.openlocfilehash: ab361c4e83ae5e2b2bb6614bdc4a513e0bdd77ed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68059002"
---
# <a name="capture-a-trace-in-database-experimentation-assistant"></a>Capture un seguimiento en el Asistente de experimentación de base de datos

Puede usar una captura de seguimiento en base de datos experimentación Assistant (DEA) para crear un archivo de seguimiento que tiene un registro de eventos de servidor capturados. Un evento de servidor capturados es un evento que se produce en un servidor específico durante un período de tiempo específico. Una captura de seguimiento debe realizarse una vez por cada servidor.

Antes de iniciar una captura de seguimiento, asegúrese de realizar copias de seguridad de todas las bases de datos de destino.

Almacenamiento en caché de consulta en SQL Server puede afectar a los resultados de evaluación. Se recomienda que reinicie el servicio de SQL Server (MSSQLSERVER) en la aplicación de servicios para mejorar la coherencia de los resultados de la evaluación.

## <a name="create-a-trace-capture"></a>Crear una captura de seguimiento

1. En DEA, seleccione el icono de menú en el menú izquierdo. En el menú expandido, seleccione **capturar seguimientos** junto al icono de cámara.

    ![Seleccione capturar seguimientos en el menú](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-capture.png)

1. En **nueva captura**, escriba o seleccione la siguiente información:

    - **Nombre de instancia de SQL Server**: Escriba un nombre para el equipo que ejecuta SQL Server en el que desea capturar un seguimiento del servidor.
    - **Nombre de la base de datos**: Escriba un nombre para una base de datos que se va a iniciar un seguimiento de la base de datos. Si no se especifica una base de datos, se captura la traza en todas las bases de datos en el servidor.
    - **Nombre de archivo de seguimiento**: Escriba un nombre para el archivo de seguimiento para la captura.
    - **Tamaño máximo de archivo (MB)** : Seleccione el tamaño de sustitución incremental de archivos. Se crea un nuevo archivo según sea necesario en el tamaño de archivo que seleccione. El tamaño recomendado de sustitución incremental es de 200 MB.
    - **Duración (en minutos)** : Seleccione el período de tiempo (en minutos) que desee que se ejecute la captura de seguimiento.
    - **Ruta de acceso para almacenar el archivo de salida de seguimiento**: Seleccione la ruta de acceso de destino para el archivo de seguimiento. 

    > [!NOTE]
    > Debe ser la ruta de acceso al archivo de seguimiento en el equipo que ejecuta SQL Server. Si el servicio SQL Server no está establecido para una cuenta específica, el servicio podría necesita permisos de escritura en la carpeta especificada para el archivo de seguimiento que se va a escribir.
    >
    >

    ![Nueva página de captura](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-inputs.png)

## <a name="start-the-trace-capture"></a>Inicie la captura de seguimiento

Después de escribir o seleccionar la información necesaria, seleccione **iniciar** para empezar a capturar seguimientos. Si la información que escribió es válida, se inicia el proceso de captura de seguimiento. En caso contrario, los cuadros de texto que tienen entradas no válidas se resaltan en rojo. 

Asegúrese de que los valores que ha seleccionado o introducido son correctos y, a continuación, seleccione **iniciar**.

Cuando finalice la captura de seguimiento en ejecución, busque el nuevo archivo de seguimiento en la ubicación del archivo que especificó en **ruta de acceso para almacenar el archivo de salida de seguimiento**. Seleccione el icono de campana en la parte inferior del menú izquierdo para supervisar el progreso de la captura.

![Captura el progreso de los seguimientos](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-progress.png)

### <a name="trace-file"></a>Archivo de seguimiento

La captura de seguimiento escribe un archivo. trc en la ubicación especificada. El archivo de seguimiento incluye los resultados de seguimiento de la actividad de una base de datos de SQL Server. Archivos TRC están diseñados para proporcionar más información sobre los errores que se detectan y notificado por SQL Server.

## <a name="frequently-asked-questions-about-trace-capture"></a>Preguntas más frecuentes acerca de la captura de seguimiento

Siguientes son algunas de las preguntas más frecuentes acerca de la captura de seguimiento en DEA.

### <a name="what-events-are-captured-when-i-run-a-trace-capture-on-a-production-database"></a>¿Qué eventos se capturan cuando ejecuto una captura de seguimiento en una base de datos de producción?

En la tabla siguiente se proporciona la lista de los datos de columna correspondiente que se recopilan para los seguimientos y eventos:
  
|Nombre del evento|Datos de texto (1)|Datos binarios (2)|Id. de base de datos (3)|Nombre de host (8)|Nombre de la aplicación (10)|Nombre de inicio de sesión (11)|SPID (12)|Hora de inicio (14)|Hora de finalización (15)|Nombre de base de datos (35)|Secuencia de eventos (51)|IsSystem (60)|  
|---|---|---|---|---|---|---|---|---|---|---|---|---|  
|**RPC: completado (10)**||*|*|*|*|*|*|*|*|*|*|*|  
|**RPC: iniciar (11)**||*|*|*|*|*|*|*||*|*|*|  
|**RPC Output Parameter (100)**|*||*|*|*|*|*|*||*|*|*|  
|**SQL: BatchCompleted (12)**|*||*|*|*|*|*|*|*|*|*|*|  
|**SQL:BatchStarting (13)**|*||*|*|*|*|*|*||*|*|*|  
|**Audit Login (14)**|*|*|*|*|*|*|*|*||*|*|*|  
|**Audit Logout (15)**|*||*|*|*|*|*|*|*|*|*|*|  
|**ExistingConnection (17)**|*|*|*|*|*|*|*|*||*|*|*|  
|**CursorOpen (53)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorPrepare (70)**|*||*|*|*|*|*|*||*|*|*|  
|**Prepare SQL (71)**|||*|*|*|*|*|*||*|*|*|  
|**Exec preparada SQL (72)**|||*|*|*|*|*|*||*|*|*|  
|**CursorExecute (74)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorUnprepare (77)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorClose (78)**|*||*|*|*|*|*|*||*|*|*|  

### <a name="is-there-a-performance-effect-on-my-production-server-when-trace-capture-is-running"></a>¿Hay un efecto de rendimiento en el servidor de producción cuando se está ejecutando la captura de seguimiento?
    
Sí, hay un efecto mínimo en el rendimiento durante la recolección de seguimiento. En nuestras pruebas, se encuentra sobre una presión de memoria de % 3.
    
### <a name="what-kind-of-permissions-are-required-for-capturing-traces-on-a-production-workload"></a>¿Qué tipo de permisos son necesarios para capturar seguimientos en una carga de trabajo de producción?
    
- El usuario de Windows que se ejecuta la operación de seguimiento en la aplicación DEA debe tener derechos de sysadmin en el equipo que ejecuta SQL Server.
- La cuenta de servicio usada en el equipo que ejecuta SQL Server debe tener acceso de escritura a la ruta de acceso del archivo de seguimiento especificado.

### <a name="can-i-capture-traces-for-the-entire-server-or-only-on-a-single-database"></a>¿Se puede capturar los seguimientos para el servidor completo o solo en una sola base de datos?
    
Puede usar DEA para capturar los rastros para todas las bases de datos en el servidor o para una sola base de datos.
    
### <a name="i-have-a-linked-server-configured-in-my-production-environment-do-those-queries-show-up-in-the-traces"></a>Tengo un servidor vinculado configurado en mi entorno de producción. ¿Esas consultas se muestra en los seguimientos?
    
Si está ejecutando una captura de seguimiento para todo el servidor, el seguimiento de captura todas las consultas, incluidas las consultas de servidor vinculado. Para ejecutar una captura de seguimiento para todo el servidor, deje el **nombre de base de datos** cuadro bajo **nueva captura** vacía.
    
### <a name="whats-the-minimum-recommended-time-for-production-workload-traces"></a>¿Qué es el tiempo mínimo recomendado para seguimientos de la carga de trabajo de producción?
    
Se recomienda que elija una hora que mejor represente la totalidad de la carga de trabajo. De este modo, el análisis se ejecuta en todas las consultas en la carga de trabajo.
    
### <a name="how-important-is-to-take-a-database-backup-right-before-i-start-a-trace-capture"></a>¿Qué tan importante es realizar una copia de seguridad de base de datos correcto antes de comenzar una captura de seguimiento?
    
Antes de iniciar una captura de seguimiento, asegúrese de que se realice una de las bases de datos de destino. Se reproduce el seguimiento capturado en el destino 1 y 2 de destino. Si el estado de la base de datos no es lo mismo, se sesga los resultados de la experimentación.

### <a name="can-i-collect-xevents-instead-of-traces-and-can-i-replay-xevents"></a>¿Puedo recopilar XEvents en lugar de los seguimientos y puedo reproducir los XEvents?
    
Sí. DEA es compatible con XEvents. Descargue la versión más reciente de DEA y pruébelo.

## <a name="troubleshoot-trace-captures"></a>Solución de problemas de capturas de seguimiento

Si ve un error al ejecutar una captura de seguimiento, revise los siguientes requisitos previos:

- Confirme que el nombre del equipo que ejecuta SQL Server es válido. Para confirmar, intente conectarse al equipo que ejecuta SQL Server utilizando SQL Server Management Studio (SSMS).
- Confirme que la configuración del firewall no bloquea las conexiones con el equipo que ejecuta SQL Server.
- Confirme que el usuario tiene los permisos que aparecen en la entrada de blog sobre [preguntas más frecuentes de reproducción](https://blogs.msdn.microsoft.com/datamigration/2017/03/24/dea-2-0-replay-faq/).
- Confirme que el nombre de seguimiento no sigue la convención estándar de sustitución incremental (capturar\_1). En su lugar, pruebe los nombres de seguimiento como captura\_1A o Capture1.

Estos son algunos posibles errores que pueden aparecer y soluciones para resolverlos:

|Posibles errores|Solución|  
|---|---|  
|No se puede iniciar el seguimiento en el destino de SQL Server, compruebe si tiene los permisos necesarios y que la cuenta de SQL Server tiene acceso de escritura a la ruta de acceso de archivo de seguimiento especificado (53) de código de Error de Sql|El usuario que ejecuta la herramienta DEA debe tener acceso al equipo que ejecuta SQL Server. El usuario debe tener asignado el rol sysadmin.|  
|No se puede iniciar el seguimiento en el destino de SQL Server, compruebe si tiene los permisos necesarios y que la cuenta de SQL Server tiene acceso de escritura a la ruta de acceso de archivo de seguimiento especificado (19062) de código de Error de Sql|La ruta de seguimiento especificada no exista o la carpeta no tiene permisos de escritura para la cuenta en qué servidor SQL Server se ejecutan los servicios (por ejemplo, servicio de red). La ruta de acceso debe existir y debe tener los permisos necesarios para iniciar la traza.|  
|Un seguimiento DEA que actualmente se está ejecutando en el servidor de destino.|Ya se está ejecutando un seguimiento activo en el servidor de destino. No se puede iniciar un nuevo seguimiento cuando un seguimiento de todo el servidor ya se está ejecutando.|  
|No se puede abrir la base de datos solicitado para la captura de seguimiento. Este error podría deberse a un nombre de base de datos incorrecta.|La base de datos especificado no existe o no es accesible para el usuario actual. Use el nombre de la base de datos correcta.|  

Si ve otros errores con la etiqueta *código de Error Sql*, consulte [los mensajes de error del sistema](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/cc645603(v=sql.105)) para obtener descripciones detalladas y resoluciones.
    
## <a name="next-steps"></a>Pasos siguientes

- Para obtener información sobre cómo configurar las herramientas de Distributed Replay en SQL Server antes de reproducir un seguimiento capturado, consulte [configurar reproducción](database-experimentation-assistant-configure-replay.md).

- Para obtener una introducción minutos 19 DEA y demostración, vea el vídeo siguiente:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
