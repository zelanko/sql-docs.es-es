---
title: OLTP en memoria (optimización en memoria) | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
helpviewer_keywords:
- In-Memory OLTP
- memory-optimized tables
ms.assetid: e1d03d74-2572-4a55-afd6-7edf0bc28bdb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6bcd8c20039b048cf717c24981124ffd61cf51f4
ms.sourcegitcommit: 6f8f975f7f97cd12fa008b05dc8d52cd1e94577f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2019
ms.locfileid: "67251005"
---
# <a name="in-memory-oltp-in-memory-optimization"></a>OLTP en memoria (optimización en memoria)

  Es una novedad en [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)], [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] puede mejorar significativamente el rendimiento de la aplicación de base de datos OLTP. [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] es un motor de base de datos optimizados para memoria integrado en el motor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], optimizado para OLTP.  
  
|||  
|-|-|  
|![Máquina Virtual de Azure](../../master-data-services/media/azure-virtual-machine.png "Máquina Virtual de Azure")|¿Quiere probar SQL Server 2016? Suscríbase a Microsoft Azure y, después, vaya **[aquí](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)** para sincronizar una máquina virtual que ya tenga SQL Server 2016 instalado. Puede eliminar la máquina Virtual cuando haya terminado.|  
  
 Para usar [!INCLUDE[hek_2](../../../includes/hek-2-md.md)], debe definir una tabla a la que se accede con mucha frecuencia como que está optimizada para memoria. Las tablas con optimización para memoria son completamente transaccionales y durables, y se accede a ellas mediante [!INCLUDE[tsql](../../../includes/tsql-md.md)] , igual que con las tablas basadas en disco. Una consulta puede hacer referencia tanto a tablas optimizadas para memoria como a tablas basadas en disco. Una transacción puede actualizar datos en tablas optimizadas para memoria y en tablas basadas en disco. Los procedimientos almacenados que solo hacen referencia a tablas optimizadas para memoria se pueden compilar de forma nativa en código máquina para obtener nuevas mejoras en el rendimiento. El motor [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] se ha diseñado para sesiones de simultaneidad muy elevada para el tipo OLTP de transacciones que se derivan de un nivel medio con gran capacidad de ampliación horizontal. Para lograr esto, usa estructuras de datos sin bloqueos temporales y control de simultaneidad optimista de múltiples versiones. El resultado es predecible, de baja latencia por debajo de los milisegundos y de gran rendimiento con escalado lineal para transacciones de bases de datos. La ganancia de rendimiento real depende de muchos factores, pero es habitual obtener un rendimiento entre 5 y 20 veces superior.  
  
 En esta tabla resumimos los patrones de carga de trabajo que sacarían el máximo partido usando [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]:  
  
|Escenario de implementación|Escenario de implementación|Ventajas de [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]|  
|-----------------------------|-----------------------------|-------------------------------------|  
|Índice elevado de inserción de datos a partir de varias conexiones simultáneas.|Almacenamiento principal solo de adición.<br /><br /> Incapaz de procesar la carga de trabajo insertada.|Eliminar contención.<br /><br /> Reducir registros.|  
|Leer el rendimiento y escalar con inserción y actualizaciones por lotes periódicos.|Operaciones de lectura de alto rendimiento, especialmente cuando cada solicitud de servidor debe realizar varias operaciones de lectura.<br /><br /> Incapaz de satisfacer los requisitos de ampliación vertical.|Eliminar la contención cuando llegan datos nuevos.<br /><br /> Recuperación de datos de menor latencia.<br /><br /> Minimizar el tiempo de ejecución del código.|  
|Procesamiento intensivo de lógica empresarial en el servidor de base de datos.|Insertar, actualizar y eliminar cargas de trabajo.<br /><br /> Cálculos que consumen muchos recursos en los procedimientos almacenados.<br /><br /> Contención de lectura y escritura.|Eliminar contención.<br /><br /> Minimizar el tiempo de ejecución del código para reducir la latencia y mejorar el rendimiento.|  
|Baja latencia.|Requerir transacciones empresariales de baja latencia que no pueden realizar las soluciones de bases de datos habituales.|Eliminar contención.<br /><br /> Minimizar el tiempo de ejecución del código.<br /><br /> Ejecución de código de baja latencia.<br /><br /> Recuperación eficaz de datos.|  
|Administración del estado de la sesión.|Inserciones, actualizaciones y búsquedas de punto frecuentes.<br /><br /> Carga de escala alta de numerosos servidores web sin estado.|Eliminar contención.<br /><br /> Recuperación eficaz de datos.<br /><br /> Opcional: reducción o eliminación de E/S cuando se usen tablas que no sean durables|  
  
 Para obtener más información acerca de los escenarios donde [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] suponga alcanzar un mayor rendimiento, consulte [OLTP en memoria: patrones de carga de trabajo comunes y consideraciones de migración](https://msdn.microsoft.com/library/dn673538.aspx).  
  
 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] mejorará el rendimiento de forma óptima en OLTP con transacciones de breve ejecución.  
  
 Entre los patrones de programación donde se apreciarán mejoras con [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] , se incluyen los escenarios de simultaneidad, búsquedas de punto, cargas de trabajo donde hay muchas inserciones y actualizaciones, y lógica empresarial en procedimientos almacenados.  
  
 La integración con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] significa que puede tener tablas optimizadas para memoria y tablas basadas en disco en la misma base de datos y realizar consultas en los dos tipos de tablas.  
  
 En [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] existen limitaciones en el área expuesta de [!INCLUDE[tsql](../../../includes/tsql-md.md)] admitida para [!INCLUDE[hek_2](../../../includes/hek-2-md.md)].  
  
 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] logra importantes mejoras en el rendimiento y la escalabilidad mediante:  
  
-   Los algoritmos que se optimizan para tener acceso a los datos residentes en memoria.  
  
-   Control de simultaneidad optimista que elimina los bloqueos lógicos.  
  
-   Objetos sin bloqueo que eliminan todos los bloqueos físicos y temporales. Subprocesos que realizan el trabajo transaccional no usan bloqueos ni bloqueos temporales para el control de simultaneidad.  
  
-   Los procedimientos almacenados compilados de forma nativa, que tienen un rendimiento bastante mejor que los procedimientos almacenados interpretados, cuando se tiene acceso a tablas optimizadas para memoria.  
  
> [!IMPORTANT]  
>  Serán necesarios algunos cambios de sintaxis en las tablas y los procedimientos almacenados para usar [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]. Para obtener más información, vea [Migrar a OLTP en memoria](migrating-to-in-memory-oltp.md). Antes de intentar migrar una tabla basada en disco a una tabla optimizada para memoria, lea [Determinar si una tabla o un procedimiento almacenado se debe pasar a OLTP en memoria](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md) para ver qué tablas y procedimientos almacenados se beneficiarán de [!INCLUDE[hek_2](../../../includes/hek-2-md.md)].  
  
## <a name="in-this-section"></a>En esta sección  
 Esta sección proporciona información acerca de los conceptos siguientes:  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Requisitos para usar tablas con optimización para memoria](memory-optimized-tables.md)|Describe los requisitos de hardware y software y las instrucciones para utilizar tablas optimizadas para memoria.|  
|[Uso de OLTP en memoria en un entorno de máquina virtual](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md)|Se ocupa del uso de [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] en entornos virtualizados.|  
|[Ejemplos de código de OLTP en memoria](in-memory-oltp-code-samples.md)|Contiene ejemplos de código en los que se muestra cómo crear y utilizar una tabla optimizada para memoria.|  
|[Memory-Optimized Tables](memory-optimized-tables.md)|Presenta las tablas optimizadas para memoria.|  
|[Variables de tabla con optimización para memoria](../../database-engine/memory-optimized-table-variables.md)|Ejemplo de código que muestra cómo utilizar una variable de tabla optimizada para memoria en lugar de una variable de tabla tradicional para reducir el uso de tempdb.|  
|[Índices de las tablas con optimización para memoria](../../database-engine/indexes-on-memory-optimized-tables.md)|Presenta los índices optimizados para memoria.|  
|[Procedimientos almacenados compilados de forma nativa](natively-compiled-stored-procedures.md)|Presenta los procedimientos almacenados compilados de forma nativa.|  
|[Administrar memoria para OLTP en memoria](../../database-engine/managing-memory-for-in-memory-oltp.md)|Descripción y administración del uso de memoria en el sistema.|  
|[Crear y administrar el almacenamiento de objetos con optimización para memoria](creating-and-managing-storage-for-memory-optimized-objects.md)|Describe los archivos delta y de datos, que almacenan información sobre las transacciones en tablas optimizadas para memoria.|  
|[Hacer copia de seguridad, restaurar y recuperar tablas con optimización para memoria](restore-and-recovery-of-memory-optimized-tables.md)|Describe las copias de seguridad, las restauraciones y las recuperaciones para tablas optimizadas para memoria.|  
|[Compatibilidad de Transact-SQL con OLTP en memoria](transact-sql-support-for-in-memory-oltp.md)|Describe la compatibilidad de [!INCLUDE[tsql](../../../includes/tsql-md.md)] para [!INCLUDE[hek_2](../../../includes/hek-2-md.md)].|  
|[Compatibilidad con alta disponibilidad para bases de datos de OLTP en memoria](high-availability-support-for-in-memory-oltp-databases.md)|Describe los grupos de disponibilidad y los clústeres de conmutación por error en [!INCLUDE[hek_2](../../../includes/hek-2-md.md)].|  
|[Compatibilidad de SQL Server con OLTP en memoria](sql-server-support-for-in-memory-oltp.md)|Enumera la sintaxis nueva y la actualizada, y las características que admiten tablas optimizadas para memoria.|  
|[Migrar a OLTP en memoria](migrating-to-in-memory-oltp.md)|Describe cómo migrar las tablas basadas en disco a tablas optimizadas para memoria.|  
  
 Encontrará más información acerca de [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] en:  
  
-   [Microsoft?? ¿SQL Server? Guía de producto de 2014](https://www.microsoft.com/download/confirmation.aspx?id=39269)  
  
-   [Blog de OLTP en memoria](https://go.microsoft.com/fwlink/?LinkId=311696)  
  
-   [OLTP en memoria y los patrones de carga de trabajo comunes y consideraciones para la migración](https://msdn.microsoft.com/library/dn673538.aspx)  
  
-   [Información general de los aspectos internos OLTP en memoria SQL Server](https://download.microsoft.com/download/8/3/6/8360731A-A27C-4684-BC88-FC7B5849A133/SQL_Server_2016_In_Memory_OLTP_White_Paper.pdf)  
    <!--
         (https://download.microsoft.com/download/8/3/6/8360731A-A27C-4684-BC88-FC7B5849A133/SQL_Server_2016_In_Memory_OLTP_White_Paper.pdf)
         (/sql/relational-databases/in-memory-oltp/sql-server-in-memory-oltp-internals-for-sql-server-2016?view=sql-server-2016)
    -->
  
## <a name="see-also"></a>Vea también  
 [Características de la base de datos](../database-features.md)  
  
  
