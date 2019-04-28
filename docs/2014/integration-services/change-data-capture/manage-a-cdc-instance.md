---
title: Administrar una instancia CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- manIns
ms.assetid: cfed22c8-c666-40ca-9e73-24d93e85ba92
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7f29463784436918834fe94c3ac5e4a8c5420703
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62835630"
---
# <a name="manage-a-cdc-instance"></a>Administrar una instancia CDC
  Puede usar la Consola del diseñador CDC para ver información acerca de las instancias que crea y para administrar el funcionamiento de las instancias.  
  
 Haga clic en el nombre de una instancia en el panel izquierdo para ver información sobre dicha instancia.  
  
> [!NOTE]  
>  Si selecciona un servicio en el panel izquierdo, la lista de instancias disponibles se muestra también en el centro de la Consola del diseñador CDC. Si selecciona una de las instancias en esta sección, puede realizar las tareas del panel derecho; sin embargo, no podrá ver la información en las pestañas de propiedades.  
  
## <a name="what-you-can-do-when-you-display-the-cdc-instance-information"></a>Qué puede hacer cuando se muestra información de la instancia CDC  
 Las acciones siguientes se realizan desde el panel derecho:  
  
 **Iniciar**  
 Haga clic en **Iniciar** para empezar a capturar cambios para la instancia CDC seleccionada.  
  
 **Detener**  
 Haga clic en **Detener** para dejar de capturar cambios para la instancia CDC seleccionada. Al detener la instancia CDC, los cambios capturados hasta ese momento no se pierden y se entregan cuando se reanuda la instancia CDC.  
  
 **Restablecer**  
 Haga clic en **Restablecer** para restablecer la instancia CDC a su estado inicial (vacío). Esta opción está disponible cuando la instancia CDC está detenida. Se eliminan todos los cambios de las tablas de cambios y el estado interno de la instancia CDC. Cuando se inicie la instancia CDC más adelante, la captura de cambios comenzará desde ese momento y solo incluirá las transacciones que comenzaron después de que se iniciara la instancia CDC.  
  
 Haga clic en **Aceptar** en el cuadro de diálogo de confirmación para confirmar que desea restablecer la instancia CDC y eliminar los cambios escritos en las tablas de cambios.  
  
 **Eliminar**  
 Haga clic en **Eliminar** para eliminar la instancia CDC de forma permanente. Esta opción solo está disponible cuando la instancia CDC está detenida.  
  
 Haga clic en **Aceptar** en el cuadro de diálogo de confirmación para confirmar que desea eliminar la instancia CDC.  
  
 **Script de registro de Oracle**  
 Haga clic en este vínculo para mostrar el cuadro de diálogo con el script de registro complementario de Oracle. Para obtener información acerca de lo que puede hacer en este cuadro de diálogo, vea [Oracle Supplemental Logging Script](oracle-supplemental-logging-script.md).  
  
> [!NOTE]  
>  Al ejecutar los scripts de registro complementario, se abre el cuadro de diálogo Credenciales de Oracle para ejecutar script donde debe proporcionar un nombre de usuario y una contraseña válidos de Oracle. Para obtener información acerca de cómo proporcionar las credenciales adecuadas de Oracle, vea [Oracle Credentials for Running Script](oracle-credentials-for-running-script.md).  
  
 **Script de implementación de instancia CDC**  
 Haga clic en este vínculo para abrir el cuadro de diálogo que muestra el script de implementación de la instancia CDC. Para obtener información acerca de este cuadro de diálogo, vea [CDC Instance Deployment Script](cdc-instance-deployment-script.md).  
  
 **Propiedades**  
 Haga clic en este vínculo para abrir el editor de propiedades. La configuración de la instancia CDC se edita mediante el editor de propiedades. Para obtener más información acerca de cómo editar las propiedades de una instancia CDC, vea [Edit Instance Properties](edit-instance-properties.md).  
  
 **Fichas del visor**  
  
 Las siguientes pestañas del visor están disponibles al ver la información de la instancia CDC. La información de estas pestañas es de solo lectura.  
  
 **Estado**  
 Esta pestaña proporciona información y estadísticas sobre el estado actual de la instancia CDC. Contiene la información siguiente.  
  
-   **Estado**: icono que indica el estado actual de la instancia CDC. A continuación se describen los estados.  
  
    |||  
    |-|-|  
    |![Error](../media/error.gif "Error")|**Error**. La instancia CDC de Oracle no se está ejecutando porque se produjo un error que no se puede reintentar. Están disponibles los subestados siguientes:<br /><br /> **Mal configurada**: se produjo un error de configuración que necesita intervención manual.<br /><br /> **Contraseña necesaria**: no se estableció ninguna contraseña para la instancia CDC de Oracle o la contraseña no es válida.<br /><br /> **Inesperado**. Todos los demás errores irrecuperables.|  
    |![Correcto](../media/okay.gif "Okay")|**En ejecución**: La instancia CDC se está ejecutando y está procesando registros de cambios. Están disponibles los subestados siguientes.<br /><br /> **Idle**: todos los registros de cambios se han procesado y se han almacenado en las tablas de cambios de destino. No hay más transacciones activas.<br /><br /> **Procesamiento**: hay registros de cambios que se están procesando que no se han escrito todavía en las tablas de cambios.|  
    |![Detener](../media/stop.gif "Detener")|**Detenido**: La instancia CDC no se está ejecutando. El estado de detenido indica que la instancia CDC se detuvo de forma normal.|  
    |![Pausado](../media/paused.gif "Pausado")|**Pausado**: la instancia CDC se está ejecutando pero el procesamiento está suspendido debido a un error que se puede reintentar. Están disponibles los subestados siguientes:<br /><br /> **Desconectado**: no se puede establecer la conexión con la base de datos Oracle de origen. El procesamiento se reanudará cuando se restaure la conexión.<br /><br /> **Almacenamiento**: el almacenamiento está lleno. El procesamiento se reanudará cuando haya más almacenamiento disponible.<br /><br /> **Registrador**: el registrador está conectado a Oracle pero no puede leer los registros de transacciones de Oracle debido a un problema temporal, por ejemplo, porque un registro de transacciones necesario no está disponible.|  
  
-   **Estado detallado**: el subestado actual.  
  
-   **Mensaje de estado**: más información sobre el estado actual.  
  
-   **Marca de tiempo**: hora UTC en que el estado CDC se leyó por última vez de la tabla de estado.  
  
-   **Procesamiento en curso**: supervise la siguiente información de esta sección.  
  
    -   **Marca de tiempo de la última transacción**: hora local de la última transacción escrita en las tablas de cambios.  
  
    -   **Marca de tiempo del último cambio**: hora local del cambio más reciente visto por la instancia CDC de Oracle en los registros de transacciones de la base de datos Oracle de origen. Esto proporciona información sobre la latencia actual de la instancia CDC en la lectura del registro de transacciones de Oracle.  
  
    -   **CN inicial del registro de transacciones**: número de cambio (CN) más reciente leído del registro de transacciones de Oracle.  
  
    -   **CN final del registro de transacciones**: número de cambio para recuperar o reiniciar la instancia CDC. La instancia CDC de Oracle volverá a colocarse en esta ubicación en caso de que se produzca un reinicio o cualquier otro tipo de error (incluida la conmutación por error de clúster).  
  
    -   **CA actual**: último número de cambio (SCN) visto en la base de datos Oracle de origen (no en el registro de transacciones).  
  
    -   **Transacciones activas**: número actual de transacciones de Oracle de origen que está procesando la instancia CDC de Oracle y que aún no se han decidido (confirmación o reversión).  
  
    -   **Transacciones almacenadas provisionalmente**: número actual de transacciones de Oracle de origen que se han almacenado provisionalmente en la tabla [cdc.xdbcdc_staged_transactions](the-oracle-cdc-databases.md#bkmk_cdcxdbcdc_staged_transactions).  
  
-   **Contadores**: supervise la siguiente información de esta sección.  
  
    -   **Transacciones completadas**: número de transacciones completadas desde que se restableció por última vez la instancia CDC. Esto no incluye las transacciones que no contienen tablas de interés.  
  
    -   **Cambios escritos**: número de cambios escritos en las tablas de cambios de SQL Server.  
  
 **Oracle**  
 Muestra información sobre la instancia CDC y su conexión con la base de datos de Oracle. Esta pestaña es de solo lectura. Para editar estas propiedades, haga clic con el botón derecho en la instancia del panel izquierdo y seleccione **Propiedades** o haga clic en **Propiedades** en el panel derecho para abrir el cuadro de diálogo Propiedades de \<instancia>.  
  
 Para obtener información acerca de estas propiedades y cómo editarlas, vea [Edit the Oracle Database Properties](edit-the-oracle-database-properties.md).  
  
 **Tablas**  
 Muestra información sobre las tablas incluidas en la instancia CDC. La información de columna también está disponible aquí. Esta pestaña es de solo lectura. Para editar estas propiedades, haga clic con el botón derecho en la instancia del panel izquierdo y seleccione **Propiedades** o haga clic en **Propiedades** en el panel derecho para abrir el cuadro de diálogo Propiedades de \<instancia>.  
  
 Para obtener información acerca de estas propiedades y cómo editarlas, vea [Edit Tables](edit-tables.md).  
  
 **Avanzadas**  
 Muestra las propiedades avanzadas para la instancia CDC y los valores de propiedad. Esta pestaña es de solo lectura. Para editar estas propiedades, haga clic con el botón derecho en la instancia del panel izquierdo y seleccione **Propiedades** o haga clic en **Propiedades** en el panel derecho para abrir el cuadro de diálogo Propiedades de \<instancia>.  
  
 Para obtener información acerca de estas propiedades y cómo editarlas, vea [Edit the Advanced Properties](edit-the-advanced-properties.md).  
  
## <a name="see-also"></a>Vea también  
 [Cómo crear la instancia de base de datos de cambios de SQL Server](how-to-create-the-sql-server-change-database-instance.md)   
 [Cómo ver las propiedades de la instancia CDC](how-to-view-the-cdc-instance-properties.md)   
 [Cómo editar las propiedades de la instancia CDC](how-to-edit-the-cdc-instance-properties.md)   
 [Usar el Asistente para nueva instancia](use-the-new-instance-wizard.md)  
