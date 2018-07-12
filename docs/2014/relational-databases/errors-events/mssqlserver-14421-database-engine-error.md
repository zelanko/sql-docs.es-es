---
title: MSSQLSERVER_14421 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 14421 (Database Engine error)
ms.assetid: 03e76d4a-d463-4673-8843-08e4ecaefe27
caps.latest.revision: 23
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 29efb64c800d74a2e9c88db06d40c55a229d731d
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37415564"
---
# <a name="mssqlserver14421"></a>MSSQLSERVER_14421
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|14421|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQLErrorNum14421|  
|Texto del mensaje|La base de datos secundaria de trasvase de registros %s.%s tiene un umbral de restauración de %d minutos y no está sincronizada. No se ha realizado ninguna operación de restauración durante %d minutos. La latencia restaurada es de %d minutos. Compruebe la información del registro de agente y del monitor de trasvase de registros.|  
  
## <a name="explanation"></a>Explicación  
 Este mensaje indica que el trasvase de registros no está sincronizado más allá del umbral de restauración. El umbral de restauración es la cantidad de minutos que pueden transcurrir entre las operaciones de restauración antes de que se genere un mensaje.  
  
### <a name="possible-causes"></a>Posibles causas  
 Este mensaje no indica necesariamente un problema en el trasvase de registros. En su lugar, puede indicar uno de los siguientes problemas:  
  
-   El trabajo de restauración no está en ejecución.  
  
     Entre las posibles causas que impiden la ejecución del trabajo se encuentran: el servicio del Agente SQL Server en la instancia del servidor secundario no se está ejecutando, el trabajo está deshabilitado o la programación del trabajo ha cambiado.  
  
-   Error en el trabajo de restauración.  
  
     Entre las posibles causas del error del trabajo se encuentran: la ruta de acceso de la carpeta de restauración no es válida, el disco está lleno o cualquier otro motivo por el que la instrucción RESTORE generó un error.  
  
## <a name="user-action"></a>Acción del usuario  
 Para solucionar el problema de este mensaje:  
  
-   Asegúrese de que el servicio del Agente SQL Server está en ejecución para la instancia del servidor secundario y que el trabajo de restauración de la base de datos secundaria está habilitado y programado para funcionar con la frecuencia adecuada.  
  
-   Es posible que exista un error en el trabajo de restauración del servidor secundario. En este caso, compruebe el historial de trabajos del trabajo de restauración para buscar la causa.  
  
-   Es posible que el trabajo de restauración del trasvase de registros, que se ejecuta en la instancia del servidor secundario, no pueda conectarse a la instancia del servidor de supervisión para actualizar la tabla **log_shipping_monitor_secondary**. Esto puede deberse a un problema de autenticación entre la instancia del servidor de supervisión y la instancia del servidor secundario.  
  
-   Es posible que el umbral de alerta de la copia de seguridad tenga un valor incorrecto. Lo ideal sería establecer este valor en el triple de la frecuencia del trabajo de restauración. Si cambia la frecuencia del trabajo de restauración después de configurar y poner en funcionamiento el trasvase de registros, debe actualizar en consecuencia el valor del umbral de alerta de la copia de seguridad.  
  
-   Cuando la instancia del servidor de supervisión se desconecta y se vuelve a conectar posteriormente, la tabla **log_shipping_monitor_secondary** no se actualiza con los valores actuales antes de que se ejecute el trabajo del mensaje de alerta. El error 14421 se puede generar cuando un trabajo de restauración concluye correctamente y se muestra: "No se pudo encontrar un archivo de copia de seguridad de registros que se pudiera aplicar a la base de datos secundaria." Cuando esto sucede, no se actualiza la hora de la restauración. Es posible que la causa del error sea, en este caso, un problema en el trabajo de copia.  
  
     Para actualizar las tablas de supervisión con los últimos datos de la base de datos secundaria, ejecute **sp_refresh_log_shipping_monitor** en la instancia del servidor secundario.  
  
-   La fecha o la hora es incorrecta en la instancia del servidor de supervisión o secundario. Esto puede generar también mensajes de alerta. Es posible que la fecha o la hora del sistema se haya modificado en uno de ellos.  
  
    > [!NOTE]  
    >  El hecho de que existan diferentes zonas horarias en las dos instancias de servidor no debería causar problemas.  
  
## <a name="see-also"></a>Vea también  
 [log_shipping_monitor_secondary &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/log-shipping-monitor-secondary-transact-sql)   
 [Acerca del trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_help_log_shipping_monitor_secondary &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-secondary-transact-sql)   
 [sp_refresh_log_shipping_monitor &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql)   
 [Acerca del trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)  
  
  
