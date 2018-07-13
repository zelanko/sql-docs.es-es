---
title: MSSQLSERVER_14420 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 14420 (Database Engine error)
ms.assetid: 4a1d72b1-ab1b-4119-a11b-a8a05c6fdb45
caps.latest.revision: 22
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 99bd3be6c0312d9e33ff0e00110db38e17a6a4dd
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37413954"
---
# <a name="mssqlserver14420"></a>MSSQLSERVER_14420
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|14420|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQLErrorNum14420|  
|Texto del mensaje|La base de datos principal de trasvase de registros %s.%s tiene un umbral de copia de seguridad de %d minutos y no ha realizado una operación de copia de seguridad del registro durante %d minutos. Compruebe la información del registro de agente y del monitor de trasvase de registros.|  
  
## <a name="explanation"></a>Explicación  
 El trasvase de registros no está sincronizado más allá del umbral de copia de seguridad. El umbral de copia de seguridad es la cantidad de minutos que pueden transcurrir entre los trabajos de copia de seguridad del trasvase de registros antes de que se genere una alerta. Este mensaje no indica necesariamente un problema en el trasvase de registros. En su lugar, puede indicar uno de los siguientes problemas:  
  
-   El trabajo de copia de seguridad no está en ejecución. Entre las posibles causas de esto se encuentran: el servicio del Agente SQL Server en la instancia del servidor principal no se está ejecutando, el trabajo está deshabilitado o la programación del trabajo ha cambiado.  
  
-   Error en el trabajo de copia de seguridad. Entre las posibles causas de esta situación se encuentran: la ruta de acceso de la carpeta de copia de seguridad no es válida, el disco está lleno o cualquier otro motivo por el que la instrucción BACKUP generara un error.  
  
## <a name="user-action"></a>Acción del usuario  
 Para solucionar el problema de este mensaje:  
  
-   Asegúrese de que el servicio del Agente SQL Server está en ejecución para la instancia del servidor principal y que el trabajo de copia de seguridad de la base de datos principal está habilitado y programado para funcionar con la frecuencia adecuada.  
  
-   Es posible que exista un error en el trabajo de copia de seguridad del servidor principal. En este caso, compruebe el historial de trabajos del trabajo de copia de seguridad para buscar la causa.  
  
-   Es posible que el trabajo de copia de seguridad del trasvase de registros, que se ejecuta en la instancia del servidor principal, no pueda conectarse a la instancia del servidor de supervisión para actualizar la tabla **log_shipping_monitor_primary**. Esto puede deberse a un problema de autenticación entre la instancia del servidor de supervisión y la instancia del servidor principal.  
  
-   Es posible que el umbral de alerta de la copia de seguridad tenga un valor incorrecto. Lo ideal sería establecer este valor en el triple de la frecuencia del trabajo de copia de seguridad. Si cambia la frecuencia del trabajo de copia de seguridad después de configurar y poner en funcionamiento el trasvase de registros, debe actualizar en consecuencia el valor del umbral de alerta de la copia de seguridad.  
  
-   Cuando la instancia del servidor de supervisión se desconecta y se vuelve a conectar posteriormente, la tabla **log_shipping_monitor_primary** no se actualiza con los valores actuales antes de que se ejecute el trabajo del mensaje de alerta. Para actualizar las tablas de supervisión con los últimos datos de la base de datos principal, ejecute **sp_refresh_log_shipping_monitor** en la instancia del servidor principal.  
  
-   La fecha o la hora es incorrecta en la instancia del servidor de supervisión o primario. Esto puede generar también mensajes de alerta. Es posible que la fecha o la hora del sistema se haya modificado en uno de ellos.  
  
    > [!NOTE]  
    >  El hecho de que existan diferentes zonas horarias en las dos instancias de servidor no debería causar problemas.  
  
## <a name="see-also"></a>Vea también  
 [log_shipping_monitor_primary &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/log-shipping-monitor-primary-transact-sql)   
 [Acerca del trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_help_log_shipping_monitor_primary &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-primary-transact-sql)   
 [sp_refresh_log_shipping_monitor &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql)   
 [Acerca del trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)  
  
  
