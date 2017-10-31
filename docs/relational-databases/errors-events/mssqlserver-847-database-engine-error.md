---
title: MSSQLSERVER_847 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 847 (Database Engine error)
ms.assetid: 67208b7c-bd8d-48a1-9f70-a6488e0f5f9b
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 16faf8a17c540e25650ce35b298895dc5704e45f
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver847"></a>MSSQLSERVER_847
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|847|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|N/A|  
|Texto del mensaje|Se agotó el tiempo de espera mientras se esperaba el bloqueo temporal: clase '%ls', id. %p, tipo %d, Tarea 0x%p : %d, tiempo de espera %d, marcas 0x%I64x, tarea propietaria 0x%p. Esperando.|  
  
## <a name="explanation"></a>Explicación  
Es posible que un equipo deje de responder o que se agote el tiempo de espera o se produzca alguna otra interrupción de las operaciones normales al mismo tiempo que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escribe errores de bloqueos temporales de búfer en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Si el campo de estado del mensaje tiene activado el valor 0x04, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estará esperando una operación de E/S. También puede recibir el mensaje [MSSQLSERVER_833](~/relational-databases/errors-events/mssqlserver-833-database-engine-error.md) en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Si el campo de estado del mensaje tiene desactivado el valor 0x04, habrá una contención intensa en una página. Si el objeto es una página de datos, esto puede deberse a un diseño de código ineficaz. Si la página no es de datos, el error puede producirse por cuellos de botella del servidor, como recursos de hardware insuficientes.  
  
## <a name="user-action"></a>Acción del usuario  
Para solucionar este problema, según el entorno, puede seguir uno o varios de estos pasos para reducir o eliminar los mensajes de error:  
  
-   Determine si tiene algún cuello de botella de hardware. Si es necesario, actualice el hardware para que sea compatible con los requisitos de configuración, consulta y carga del entorno. Para obtener más información sobre los cuellos de botella, vea [Identificar los cuellos de botella](~/relational-databases/performance/identify-bottlenecks.md).  
  
-   Compruebe si hay algún error registrado y ejecute los diagnósticos suministrados por el proveedor de hardware.  
  
-   Asegúrese de que las unidades de disco no estén comprimidas. No se admite el almacenamiento de datos ni archivos de registro en unidades comprimidas. Para obtener más información sobre los archivos físicos, vea [Archivos y grupos de archivos de base de datos](~/relational-databases/databases/database-files-and-filegroups.md).  
  
-   Observe si los mensajes de error desaparecen al desactivar las siguientes opciones:  
  
    -   Opción de configuración de aumento de prioridad de SQL Server  
  
    -   Opción de agrupación ligera (modo de fibra)  
  
    -   Opción "set working set size"  
  
    > [!NOTE]  
    > A menudo, las opciones de configuración anteriores pueden ser contraproducentes si modifica su valor predeterminado desactivado. Para obtener más información, vea [Opciones de configuración del servidor &#40;SQL Server&#41;](~/database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
-   Optimice las consultas para reducir los recursos utilizados en el sistema. La optimización del rendimiento ayudará a reducir la demanda en un sistema y a mejorar el tiempo de respuesta de las consultas individuales.  
  
-   Establezca la opción AUTO_SHRINK en OFF para reducir la sobrecarga de los cambios de tamaño de la base de datos.  
  
-   Asegúrese de establecer la opción FILEGROWTH en incrementos lo suficientemente grandes como para ser infrecuentes. Programe un trabajo para comprobar el espacio disponible en las bases de datos y, a continuación, aumente el tamaño de la base de datos durante las horas de menor actividad.  
  

