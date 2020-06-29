---
title: Instancia Oracle CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ed71e8c4-e013-4bf2-8b6c-1e833ff2a41d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a9f4b99c65ef2a3927ee31380e7931209830841a
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85435272"
---
# <a name="the-oracle-cdc-instance"></a>La instancia CDC de Oracle
  La instancia CDC de Oracle es un proceso creado por el servicio CDC de Oracle para procesar los cambios capturados a partir de una sola base de datos de origen de Oracle. La instancia CDC de Oracle recupera su configuración de la tabla **cdc.xdbcdc_config** y mantiene su estado en la tabla **cdc.xdbcdc_state** . Estas tablas forman parte de la base de datos CDC, que define la instancia CDC de Oracle. Para obtener más información acerca de la base de datos y las tablas xdbcdc, vea [The CDC Databases](the-oracle-cdc-service.md).  
  
 A continuación se describen las tareas que realiza la instancia CDC de Oracle:  
  
-   **Comprobar el inicio del servicio**: cuando se inicia, la instancia CDC carga su configuración desde la tabla **xdbcdc_config** y realiza una serie de comprobaciones de estado que se aseguran de que el estado almacenado de la instancia CDC sea coherente y que puede empezar a procesar cambios.  
  
-   **Preparar la captura de cambios**: cuando la comprobación se realiza correctamente, la instancia CDC de Oracle examina todas las instancias de captura definidas actualmente y prepara las consultas de Oracle LogMiner y otras estructuras auxiliares necesarias para la captura de cambios. Además, la instancia de Oracle vuelve a cargar el estado interno de captura que se guardó la última vez que se ejecutó la instancia CDC de Oracle.  
  
-   **Capturar cambios desde Oracle**: la instancia CDC de Oracle agrupa los cambios de Oracle mediante Oracle LogMiner, los ordena según la confirmación de la transacción y después cambia el tiempo en una transacción y los escribe en las tablas de cambios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos CDC.  
  
-   **Administrar el cierre del servicio**: el servicio CDC de Oracle administra el ciclo de vida de la instancia CDC de Oracle. Cuando se solicita el cierre de la instancia CDC de Oracle, realiza las tareas siguientes:  
  
    -   Deja de leer desde el registro de transacciones de Oracle.  
  
    -   Deja de escribir las transacciones completadas de Oracle en la base de datos CDC.  
  
    -   Espera hasta 30 segundos (si es necesario) hasta que la transacción actual termina de escribir en la base de datos CDC. Si transcurren más de 30 segundos, se cancela la escritura y se revierte la transacción (se volverá a intentar cuando se reinicie la instancia CDC).  
  
    -   En un subproceso independiente, escribe en la tabla de transacciones de ensayo todos los registros almacenados en caché posibles durante un máximo de 30 segundos (de la transacción más antigua a la más reciente), actualiza la tabla **xdbcdc_state** y confirma todos los cambios.  
  
-   **Administrar los cambios de configuración**: la instancia CDC de Oracle recibe una notificación de los cambios de configuración por parte del servicio CDC o mediante la detección de una nueva versión de la tabla **cdc.xdbcdc_config** . La mayoría de los cambios no necesitan que se reinicie la instancia CDC de Oracle (por ejemplo, agregar o quitar instancias de captura). Sin embargo, algunos cambios (como cambiar las credenciales de acceso o la cadena de conexión de Oracle) sí hacen necesario el reinicio de la instancia CDC.  
  
-   **Administrar la recuperación**: cuando se inicia una instancia CDC de Oracle, su estado interno se restaura desde las tablas **xdbcdc_state** y **xdbcdc_staged_transactions** . Una vez restaurado el estado, la instancia CDC continúa de la forma habitual.  
  
## <a name="see-also"></a>Consulte también  
 [Tratamiento de errores](error-handling.md)  
  
  
