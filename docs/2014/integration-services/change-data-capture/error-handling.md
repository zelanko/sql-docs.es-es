---
title: Tratamiento de errores | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ff79e19d-afca-42a4-81b0-62d759380d11
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 938d32c65c8eb1d7fa6087d864e62b0bb4d5d388
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204029"
---
# <a name="error-handling"></a>Tratamiento de errores
  Una instancia CDC de Oracle realiza minería de datos en los cambios de una sola base de datos de origen de Oracle (un clúster de Oracle RAC se considera una sola base de datos) y escribe los cambios confirmados en las tablas de cambios en una base de datos CDC en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino.  
  
 Una instancia CDC mantiene su estado en una tabla del sistema denominada **cdc.xdbcdc_state**. Esta tabla se puede consultar en cualquier momento para conocer el estado de la instancia CDC. Para obtener más información sobre la tabla cdc.xdbcdc_state, vea [cdc.xdbcdc_state](the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_state).  
  
 En la tabla siguiente se describen los estados de la instancia CDC en la tabla xdbcdc_state.  
  
 Para cada estado, se muestran las dos indicaciones siguientes para las columnas correspondientes de la tabla cdc.xdbcdc_state:  
  
-   La instancia no está activa (no hay ningún proceso de Windows que la administra actualmente). Si el valor de la columna **active** es 1, se está ejecutando un subproceso del servicio CDC de Oracle que administra esta instancia CDC de Oracle específica.  
  
-   Si el valor de la columna **error** es 0, la instancia CDC de Oracle no está en una condición de error. Si el valor de la columna **error** es 1, hay un error que impide que la instancia CDC de Oracle procese cambios.  
  
     Si la columna **error** tiene el valor 1 y el valor de la columna **active** es también 1, se está produciendo un error recuperable para la instancia CDC de Oracle, que se puede resolver automáticamente. Si la columna error tiene un valor de 1 y la columna active tiene el valor 0, en la mayoría de los casos puede ser necesaria una solución manual para resolver el problema antes de que el procesamiento se puede reanudar.  
  
 En la tabla siguiente se describen los distintos códigos de estado que la instancia CDC de Oracle puede notificar en su tabla de estado.  
  
|Estado|Código de estado de active|Código de estado de error|Descripciones|  
|------------|------------------------|-----------------------|------------------|  
|ABORTED|0|1|La instancia CDC de Oracle no se está ejecutando. El subestado ABORTED indica que la instancia CDC de Oracle estaba ACTIVE y se ha detenido inesperadamente.<br /><br /> La instancia principal del servicio CDC de Oracle establece el subestado ABORTED cuando detecta que la instancia CDC de Oracle no se está ejecutando mientras su estado es ACTIVE.|  
|error|0|1|La instancia CDC de Oracle no se está ejecutando. El estado ERROR indica que la instancia CDC estaba ACTIVE pero encontró un error no recuperable y se deshabilitó a sí misma. El estado ERROR contiene los códigos de subestado siguientes:<br /><br /> MISCONFIGURED: se detectó un error de configuración irrecuperable.<br /><br /> PASSWORD-REQUIRED: no hay ninguna contraseña establecida en el Diseñador de captura de datos modificados para Oracle de Attunity o la contraseña configurada no es válida. Esto puede deberse a un cambio en la contraseña de clave asimétrica del servicio.|  
|RUNNING|1|0|La instancia CDC se está ejecutando y está procesando registros de cambios. El estado RUNNING contiene los códigos de subestado siguientes:<br /><br /> IDLE: todos los registros de cambios se han procesado y almacenado en las tablas de control de destino (**_CT**). No hay ninguna transacción activa con las tablas de control.<br /><br /> PROCESSING: hay registros de cambios que se están procesando y que no se han escrito todavía en las tablas de control (**_CT**).|  
|STOPPED|0|0|La instancia CDC no se está ejecutando. El subestado STOP indica que la instancia CDC estaba ACTIVE y se detuvo correctamente.|  
|SUSPENDED|1|1|La instancia CDC se está ejecutando pero el procesamiento está suspendido debido a un error recuperable. El estado SUSPENDED contiene los códigos de subestado siguientes:<br /><br /> DISCONNECTED: no se puede establecer la conexión con la base de datos de Oracle de origen. El procesamiento se reanudará una vez que se restaure la conexión.<br /><br /> STORAGE: el almacenamiento está lleno. El procesamiento se reanudará cuando haya disponible más almacenamiento. En algunos casos, este estado puede no aparecer porque la tabla de estado no se puede actualizar.<br /><br /> LOGGER: el registrador está conectado a Oracle pero no puede leer los registros de transacciones de Oracle debido a un problema temporal.|  
|DATAERROR|x|x|Este código de estado solo se usa para la tabla **xdbcdc_trace** . No aparece en la tabla **xdbcdc_state** . Los registros de seguimiento que tienen este estado indican un problema con una entrada de registro de Oracle. La entrada de registro no válida se almacena en la columna **data** como un BLOB. El estado DATAERROR contiene los códigos de subestado siguientes:<br /><br /> BADRECORD: la entrada de registro adjunta no se pudo analizar.<br /><br /> CONVERT-ERROR: los datos de algunas columnas no se pudieron convertir a las columnas de destino de la tabla de captura. Este estado puede aparecer solo si la configuración especifica que los errores de conversión deben producir registros de seguimiento.|  
  
 Puesto que el estado del servicio CDC de Oracle se almacena en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede haber casos en los que el valor de estado de la base de datos no refleje el estado actual del servicio. El escenario más común es cuando el servicio pierde su conexión con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y no se puede reanudar (por cualquier motivo). En ese caso, el estado almacenado en **cdc.xdbcdc_state** se queda obsoleto. Si la marca de tiempo (UTC) de la última actualización tiene más de un minuto de antigüedad, probablemente el estado esté obsoleto. En este caso, use el Visor de eventos de Windows para buscar información adicional sobre el estado del servicio.  
  
## <a name="error-handling"></a>Tratamiento de errores  
 En esta sección se describe cómo trata los errores el servicio CDC de Oracle.  
  
### <a name="logging"></a>Registro  
 El servicio CDC de Oracle crea información de error en uno de los lugares siguientes.  
  
-   El registro de eventos de Windows, que se emplea con los errores de registro y para indicar eventos del ciclo de vida del servicio CDC de Oracle (iniciar, detener, conectar o volver a conectar con la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino).  
  
-   La tabla MSXDBCDC.dbo.xdbcdc_trace, que el proceso principal del servicio CDC de Oracle emplea para el registro y el seguimiento generales.  
  
-   La tabla \<cdc-database>.cdc.xdbcdc_trace, que las instancias Oracle CDC usan para el registro y el seguimiento generales. Esto significa que los errores relacionados con una instancia CDC de Oracle específica se registran en la tabla de seguimiento de esa instancia.  
  
 El servicio CDC de Oracle registra información cuando el servicio:  
  
-   Es iniciado o detenido por el administrador de control de servicios.  
  
-   No se puede conectar con la instancia asociada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y cuando establece correctamente una conexión después de un error.  
  
-   Detecta un error al iniciar instancias de servicio CDC de Oracle.  
  
-   Detecta que una instancia CDC de Oracle se ha anulado.  
  
-   Detecta un error inesperado.  
  
 La instancia CDC registra información cuando la instancia:  
  
-   Se habilita o deshabilita.  
  
-   Detecta un error.  
  
-   Se recupera de un error recuperable.  
  
 La tabla de seguimiento también se usa para registrar información de seguimiento detallada para la solución de problemas.  
  
### <a name="handling-source-oracle-connection-errors"></a>Controlar los errores de conexión de Oracle de origen  
 El servicio CDC de Oracle necesita una conexión persistente con la base de datos de Oracle de origen. Muchos errores de conexión que no están relacionadas con la configuración del servicio (como errores de red) se consideran transitorios. Por tanto, si el servicio CDC de Oracle no puede establecer conexión con la base de datos de Oracle (en el inicio o durante el trabajo que sigue a una desconexión), el servicio cambia su estado a SUSPENDED/DISCONNECTED y entra en un bucle de reintentos en el que la conexión se vuelve a intentar periódicamente. Cuando se restablece la conexión, el procesamiento continúa.  
  
 Otros tipos de errores de conexión no son transitorios (por ejemplo, credenciales no válidas, privilegios insuficientes y una dirección de base de datos no válida). Cuando se producen estos errores, el estado del servicio CDC de Oracle se establece en ERROR/MISCONFIGURED o en ERROR/PASSWORD-REQUIRED y el servicio se deshabilita. Cuando el usuario corrige el error subyacente, la instancia CDC de Oracle debe volver a habilitarse manualmente para que el procesamiento se reanude.  
  
 Cuando no está claro si el error es transitorio, lo mejor es suponer que es transitorio.  
  
### <a name="handling-target-sql-server-connection-errors"></a>Controlar errores de conexión con SQL Server de destino  
 El servicio CDC de Oracle necesita una conexión persistente con la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino. Esta conexión se emplea para:  
  
-   Asegurarse de que no haya otros servicios con el mismo nombre que usen actualmente esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Comprobar que la instancia CDC de Oracle está habilitada o deshabilita e iniciar (o detener) su subproceso.  
  
 Cuando el servicio establece una conexión con la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino y comprueba que es el único servicio CDC de Oracle con este nombre que está funcionando, puede comprobar qué instancias CDC de Oracle están habilitadas e iniciar sus procesos de control (después el servicio detiene estos procesos cuando se deshabilitan). Las instancias CDC de Oracle usan sus conexiones con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para trabajar con la base de datos CDC de la instancia CDC de Oracle.  
  
 La forma en que se controlan los errores en la conexión con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino depende de si los errores son transitorios o no.  
  
 En el caso de los errores no transitorios conocidos (como credenciales no válidas, privilegios insuficientes, información de conexión incorrecta), el servicio registra un error en el registro de eventos de Windows y se detiene (no puede escribir en la tabla de seguimiento porque no puede conectar con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]). En este caso, el usuario debe resolver el error y reiniciar el servicio de Windows CDC de Oracle.  
  
 Si se trata de errores transitorios y errores inesperados, la operación se reintenta varias veces y si el error persiste durante un período de tiempo significativo, el servicio CDC detiene sus subprocesos de instancia CDC y vuelve al intento de conexión inicial (para entonces, un servicio CDC de Oracle de otro equipo puede haber tomado ya el control de ese servicio CDC).  
  
### <a name="handling-target-sql-server-storage-full-errors"></a>Controlar errores de almacenamiento lleno de SQL Server de destino  
 Cuando el servicio CDC de Oracle detecta que no puede insertar nuevos datos modificados en la base de datos CDC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino, escribe una advertencia en el registro de eventos e intenta insertar un registro de seguimiento (aunque se puede producir un error por el mismo motivo). A continuación, vuelve a intentar la operación en un intervalo determinado hasta que lo consigue.  
  
### <a name="handling-oracle-cdc-errors"></a>Controlar errores CDC de Oracle  
 La instancia CDC de Oracle lee el registro de transacciones de Oracle y lo procesa. Si el procesamiento de CDC detecta un error, se notifica en la tabla **cdc.xdbcdc_state** y el usuario debe intervenir manualmente según el error notificado.  
  
 Por ejemplo, puede que la instancia CDC de Oracle no esté activa durante un tiempo prolongado y los archivos de registro de transacciones de Oracle necesarios ya no estén disponibles. En este caso, el DBA de Oracle debe restaurar los registros necesarios para que la instancia CDC de Oracle reanude el procesamiento.  
  
### <a name="handling-unexpected-oracle-cdc-instance-failures"></a>Controlar errores inesperados de la instancia CDC de Oracle  
 El servicio CDC de Oracle supervisa los subprocesos de la instancia CDC. Cuando se anula un subproceso de instancia CDC, el servicio CDC lo deshabilita en la tabla MSXDBCDC.dbo.xdbcdc_databases y actualiza su estado de cdc.xdbcdc_state a ABORTED. En este caso, se emplea el cuadro de diálogo estándar de informe de errores de Windows para informar del error para su análisis.  
  
## <a name="see-also"></a>Vea también  
 [Diseñador de captura de datos modificados para Oracle de Attunity](change-data-capture-designer-for-oracle-by-attunity.md)   
 [La instancia CDC de Oracle](the-oracle-cdc-instance.md)  
  
  