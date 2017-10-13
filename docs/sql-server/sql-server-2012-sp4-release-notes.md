---
title: "Notas de la versión de SQL Server 2012 SP4 | Microsoft Docs"
ms.prod: sql-server-2012
ms.technology: server-general
ms.custom: 
ms.date: 10/05/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 67cb8b3e-3d82-47f4-840d-0f12a3bff565
caps.latest.revision: 0
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: bc1321dd91a0fcb7ab76b207301c6302bb3a5e64
ms.openlocfilehash: 1d637aa3e820f1acd6dc283030d2cdfa1e6ca074
ms.contentlocale: es-es
ms.lasthandoff: 10/06/2017

---
# <a name="sql-server-2012-sp4-release-notes"></a>Notas de la versión de SQL Server 2012 SP4
En este tema se resumen las mejoras incluidas en SQL Server 2012 SP4. También se describen cuestiones que se deben revisar antes de instalar o de solucionar problemas de instalación de SP4. Las notas de la versión solo están disponibles en Internet, no se incluyen en el disco de instalación. Este tema se actualiza periódicamente, conforme se van detectando nuevos problemas. Para obtener una lista detallada de correcciones de SP4, vea [Notas de las versión de SQL Server 2012 SP4](https://go.microsoft.com/fwlink/?linkid=846937).  

> El Service Pack 4 incluye todas las actualizaciones acumulativas de SQL Server 2012 SP3.
  
##<a name="download-pages"></a>Páginas de descarga
Los siguientes artículos llevan a los paquetes de descarga principales de SQL Server 2012 SP3. Las páginas de descarga contienen los requisitos del sistema e instrucciones básicas para la instalación.
- [Instalación de la revisión SQL Server 2012 SP4](https://go.microsoft.com/fwlink/?linkid=846829)
- [SQL Server 2012 SP4 Express](https://go.microsoft.com/fwlink/?linkid=846905)
- [Microsoft SQL Server 2012 SP4 Feature Pack](https://go.microsoft.com/fwlink/?linkid=846907)

##  <a name="sp4-performance-and-scale-improvements"></a>Mejoras de rendimiento y escalado de SP4

- **Procedimiento de limpieza del agente de distribución mejorado**: una base de datos de distribución demasiado grande ha provocado la situación de bloqueo e interbloqueo. Un procedimiento de limpieza mejorado aspira a eliminar algunos de estos escenarios de bloqueo o interbloqueo. 
- **Escalado de objetos de memoria dinámico**: partición dinámica de objetos de memoria según el número de nodos y núcleos para escalar en hardware moderno. El objetivo de la promoción dinámica es evitar posibles cuellos de botella y realizar automáticamente la partición de un objeto de memoria seguro para subprocesos. Los objetos de memoria no particionados se pueden promocionar de forma dinámica para particionarse por nodo. El número de particiones es igual al número de nodos NUMA. Los objetos de memoria particionados por nodo se pueden promocionar aún más para particionarse por CPU, donde el número de particiones es igual al número de CPU.
- **Habilitar > 8TB para grupo de búferes**: habilita el espacio de direcciones virtual de 128 TB para uso por parte del grupo de búferes
- **Limpieza de Change Tracking**: rendimiento y eficacia mejorados de limpieza del seguimiento de cambios para tablas de Change Tracking. 

## <a name="sp4-supportability-and-diagnostics-improvements"></a>Mejoras de compatibilidad y diagnóstico de SP4

- **Compatibilidad de volcados de memoria completos con los agentes de replicación**: en este momento si los agentes de replicación detectan una excepción no controlada, el comportamiento predeterminado es crear un minivolcado de los síntomas de la excepción. El comportamiento predeterminado exige complejos pasos de solución de problemas para las excepciones no controladas. SP4 presenta una nueva clave del Registro que admite la creación de un volcado completo para los agentes de replicación.
- **Diagnósticos mejorados en el plan de presentación XML**: el plan de presentación XML se ha mejorado para exponer información sobre las marcas de seguimiento habilitadas, las fracciones de memoria para la combinación de bucle anidado optimizada, el tiempo de CPU y el tiempo transcurrido. 
- **Mejor correlación entre DMV y XE de diagnóstico**: los campos query_hash y query_plan_hash se usan para identificar una consulta de forma exclusiva. DMV los define como varbinary (8), mientras que XEvent los define como UINT64. Puesto que SQL Server no tiene "bigint sin signo", la conversión no siempre funciona. Esta mejora presenta nuevas columnas de filtro o acción XEvent equivalentes a query_hash y query_plan_hash, salvo que se definen como INT64, lo que puede ayudar a correlacionar consultas entre XE y DMV. 
- **Mejores diagnósticos de concesión o uso de memoria**: nuevo XEvent query_memory_grant_usage (actualización retroactiva desde Server 2016 SP1)
- **Adición de seguimiento de protocolos a los pasos de negociación SSL**: agrega información de seguimiento de bits de negociación correcta o errónea, incluido el protocolo, etc. Puede ser útil a la hora de solucionar problemas de escenarios de conectividad mientras, por ejemplo, se implementa TLS 1.2
- **Establecimiento del nivel de compatibilidad correcto para la base de datos de distribución**: después de la instalación del Service Pack, cambia el nivel de compatibilidad de la base de datos de distribución a 90. El cambio de nivel se debe a un problema en el procedimiento almacenado sp_vupgrade_replication. Ahora el SP se ha modificado para establecer el nivel de compatibilidad correcto para la base de datos de distribución. 
- **Nuevo comando DBCC para clonar una base de datos**: Base de datos clonada es un nuevo comando DBCC agregado que permite a los usuarios avanzados, como CSS, solucionar problemas de bases de datos de producción existentes mediante la clonación del esquema y los metadatos, sin los datos. La llamada se realiza con clonedatabase de DBCC (‘source_database_name’, ‘clone_database_name’). Las bases de datos clonadas no se deben usar en entornos de producción. Para ver si una base de datos se ha generado a partir de una llamada a la base de datos clonada, puede usar el comando siguiente, select DATABASEPROPERTYEX('clonedb', 'isClone'). El valor devuelto de 1 es true y 0 es false. 
- **Información del archivo TempDB y del tamaño de archivo en el registro de errores de SQL**: si el tamaño y el crecimiento automático es diferente para los archivos de datos de TempDB durante el inicio, imprime el número de archivos y desencadena una advertencia.
- **IFI admite mensajes en el registro de errores de SQL Server**: indica en el registro de errores que la inicialización instantánea de archivos de base de datos está habilitada o deshabilitada
- **Nueva DMF para reemplazar a DBCC INPUTBUFFER**: se ha presentado una nueva función de administración dinámica sys.dm_input_buffer que toma session_id como parámetro para reemplazar a DBCC INPUTBUFFER
- **Mejora de XEvents para el error de enrutamiento de lectura de un grupo de disponibilidad**: actualmente el XEvent read_only_rout_fail solo se desencadena si hay una lista de enrutamiento, pero ninguno de los servidores de la lista de enrutamiento está disponible para las conexiones. Esta mejora incluye información adicional para ayudar a solucionar el problema y además se expande en los puntos de código donde se desencadena el XEvent. 
- **Mejora del control de Service Broker con conmutación por error de grupo de disponibilidad**: actualmente, cuando Service Broker está habilitado en bases de datos de un grupo de disponibilidad, durante una conmutación por error del grupo de disponibilidad se dejan abiertas todas las conexiones de Service Broker originadas en la réplica principal. La mejora cierra todas estas conexiones abiertas durante una conmutación por error del grupo de disponibilidad.
- **[Creación de particiones de soft-NUMA automática](https://msdn.microsoft.com/library/ms345357(SQL.120).aspx)**: con SQL 2014 SP2, se presenta soft-NUMA automática cuando la marca de seguimiento 8079 está habilitada en el nivel de servidor. Cuando la marca de seguimiento 8079 está habilitada durante el inicio, SQL Server 2014 SP2 interroga al diseño de hardware y configura automáticamente soft-NUMA en los sistemas que notifican ocho o más CPU por nodo NUMA. El comportamiento de soft-NUMA automática reconoce el hiperproceso (procesador HT/lógico). La creación de particiones y la creación de nodos adicionales escala el procesamiento en segundo plano al aumentar el número de agentes de escucha, escalado y capacidades de red y cifrado. Se recomienda probar primero el rendimiento de la carga de trabajo con soft-NUMA automática antes de activarla en producción.

## <a name="see-also"></a>Vea también
- [Instalar actualizaciones de servicio de SQL Server 2012](https://msdn.microsoft.com/library/hh479746(v=sql.110).aspx)
- [Identificar la versión y edición de SQL Server](https://support.microsoft.com/en-us/help/321185)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
