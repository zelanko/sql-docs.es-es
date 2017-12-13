---
title: Alta disponibilidad y escalabilidad en Analysis Services | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d7040a55-1e4d-4c24-9333-689c1b9e2db8
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 1a1f8208a30e1ff24e76465fd9210a60ef1ec849
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="high-availability-and-scalability-in-analysis-services"></a>Alta disponibilidad y escalabilidad en Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Este artículo describen las técnicas utilizadas con más frecuencia para lograr bases de datos de Analysis Services alta disponibilidad y escalabilidad. Aunque ambos aspectos podrían abordarse por separado, la realidad es que van frecuentemente de la mano. Así, una implementación escalable para grandes cargas de trabajo de procesamiento o de consulta normalmente conlleva una disponibilidad elevada.  
  
 Pero esto no sucede a la inversa. Una alta disponibilidad, sin escala, puede ser perfectamente el único objetivo cuando existen contratos de nivel de servicio muy estrictos para cargas de trabajo de consulta de tamaño moderado, pero críticos.  
  
 Las técnicas para conseguir una alta disponibilidad y escalabilidad de Analysis Services suelen ser las mismas en todos los modos de servidor (multidimensional, tabular y modo integrado de SharePoint). A menos que se indique expresamente lo contrario, considere la información recogida en este artículo como válida para todos los modos.  
  
## <a name="key-points"></a>Puntos clave  
 Dado que las técnicas de disponibilidad y escalado difieren de las del motor de base de datos relacional, conviene hacer un breve resumen de los puntos clave a modo de introducción de las técnicas empleadas con Analysis Services:  
  
-   Analysis Services usa los mecanismos de alta disponibilidad y escalabilidad integrados en la plataforma Windows Server, a saber, el equilibrio de carga de red (NLB), los clústeres de conmutación por error de Windows Server (WSFC) o ambos.  
  
    > [!NOTE]  
    >  La característica AlwaysOn del motor de base de datos relacional no es ampliable a Analysis Services.  Una instancia de Analysis Services no se puede configurar para ejecutarse en un grupo de disponibilidad AlwaysOn.  
    >   
    >  Aunque Analysis Services no se puede ejecutar en Grupos de disponibilidad AlwaysOn, sí puede recuperar y procesar datos de las bases de datos relacionales de AlwaysOn. Para obtener instrucciones sobre cómo configurar una base de datos relacional de alta disponibilidad de modo que Analysis Services pueda usarla, consulte [Analysis Services con grupos de disponibilidad AlwaysOn](../../database-engine/availability-groups/windows/analysis-services-with-always-on-availability-groups.md).  
  
-   La alta disponibilidad, como único objetivo, se puede lograr a través de la redundancia de servidores en un clúster de conmutación por error, ya que se supone que los nodos de reemplazo tienen una configuración de hardware y software idéntica a la del nodo activo.  Los clústeres de conmutación por error de Windows Server ya ofrecen de por sí alta disponibilidad, pero sin escala.  
  
-   La escalabilidad, con o sin disponibilidad, se consigue con el equilibrio de carga de red en bases de datos de solo lectura.  La escalabilidad suele ser un problema cuando los volúmenes de consulta son grandes o están sujetos a picos repentinos.  
  
     El equilibrio de carga unido a varias bases de datos de solo lectura ofrece escala y una alta disponibilidad, ya que todos los nodos están activos y, cuando un servidor deja de funcionar, se redistribuyen solicitudes automáticamente entre el resto de nodos. Cuando se necesita tanto disponibilidad como escalabilidad, un clúster NLB es la elección correcta.  
  
 De cara al procesamiento, los objetivos de alta disponibilidad y escalabilidad no son tan importantes, puesto que el tiempo y el ámbito de las operaciones están controlados. El procesamiento puede ser parcial e incremental en determinadas partes de un modelo, pero en algún momento será necesario procesar un modelo por completo en un único servidor para garantizar que los datos de todos los índices y agregaciones son coherentes. Una arquitectura escalable sólida se basa en hardware capaz de realizar un procesamiento completo con la cadencia que sea necesaria. En soluciones de gran tamaño, esta tarea se plantea como una operación independiente con sus propios recursos de hardware.  
  
##  <a name="bkmk_serverconfig"></a> Configuración de servidor único frente a configuración multiservidor  
 En una implementación de servidor único normal, las cargas de trabajo de procesamiento y consulta se ejecutan al mismo tiempo, siempre y cuando haya recursos del sistema suficientes para ambas actividades. Analysis Services conserva intactas las estructuras de datos existentes para poder realizar consultas mientras se procesa una versión actualizada en segundo plano. Disponer de suficiente memoria y espacio en disco para administrar las estructuras de datos temporales es un requisito de hardware presente en todos los modos de servidor, si bien cada modo plantea distintas demandas de recursos del sistema y muestran diferentes niveles de compatibilidad con NUMA.  
  
 **Servidores únicos y escalabilidad**  
  
 Un solo servidor de gama alta y núcleo múltiple puede proporcionar suficiente escala por sí mismo. En un sistema de gama alta con un gran número de núcleos, RAM y espacio en disco, probablemente se pueda escalar dentro de un único sistema.  
  
 En las bases de datos multidimensionales, se pueden ajustar las propiedades de configuración de servidor para crear afinidad entre procesos y procesadores. Consulte [Thread Pool Properties](../../analysis-services/server-properties/thread-pool-properties.md) para obtener más información.  
  
 **Implementaciones multiservidor**  
  
 A veces, los requisitos operativos son los que determinan el uso de varios servidores. Por ejemplo, los clústeres de conmutación por error son multiservidor por definición, con cada nodo ejecutándose en configuraciones de hardware y software idénticas.  
  
 De forma similar, un requisito de peso para la alta disponibilidad de cargas de trabajo de consulta suele ser la existencia de varios servidores. En este escenario, la configuración recomendada en Analysis Services es ejecutar bases de datos de solo lectura y de lectura y escritura en instancias independientes de Analysis Services, en un hardware dedicado. Las bases de datos de solo lectura se encargan de las solicitudes de consulta, mientras que las de lectura y escritura se usan para el procesamiento. En la siguiente sección encontrará una descripción pormenorizada de esta técnica ampliamente usada.  
  
 **Máquinas virtuales y alta disponibilidad**  
  
 Otra estrategia para satisfacer un requisito de alta disponibilidad puede conllevar el uso de máquinas virtuales. Si la disponibilidad se puede lograr teniendo preparado un servidor de reemplazo en horas en lugar de minutos, se podrían usar máquinas virtuales que pudieran iniciarse bajo demanda y cargadas con bases de datos actualizadas recuperadas de una ubicación central.  
  
## <a name="scalability-using-read-only-and-read-write-databases"></a>Escalabilidad mediante bases de datos de solo lectura y de lectura y escritura  
 Se recomienda usar el equilibrio de carga de red en cargas de trabajo de procesamiento y consulta elevadas o que escalan. Las bases de datos de Analysis Services de una solución de NLB se definen como bases de datos de solo lectura para mantener la coherencia entre las consultas.  
  
 Aunque las instrucciones del artículo del 2008 [Scale-out querying for Analysis Services using read-only databases](https://technet.microsoft.com/library/ff795582\(v=sql.100\).aspx) (Escalar horizontalmente consultas de Analysis Services con bases de datos de solo lectura) están desfasadas, siguen siendo válidas todavía. Si bien el hardware de equipo y los sistemas operativos de servidor han evolucionado y las referencias a plataformas específicas y límites de CPU están obsoletas, la técnica básica consistente en usar bases de datos de solo lectura y de lectura y escritura en grandes volúmenes de consultas permanece inalterada.  
  
 Dicho método se puede resumir de la siguiente manera:  
  
-   Use hardware dedicado e instancias de Analysis Services para procesar la base de datos. Establezca la base de datos como de solo lectura cuando el procesamiento haya terminado. Para obtener instrucciones, vea [Switch an Analysis Services database between ReadOnly and ReadWrite modes](../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md) .  
  
-   Use varios servidores de consulta idénticos para ejecutar copias de la misma base de datos de solo lectura de Analysis Services. Los servidores se implementan en un clúster NLB, al que se obtiene acceso con un nombre de servidor virtual que actúa como único punto de entrada al clúster.  
  
-   Use Robocopy para copiar un directorio de datos entero desde el servidor de procesamiento en cada servidor de consultas y adjuntar la misma base de datos en modo de solo lectura a todos los servidores de consultas. También puede usar instantáneas de SAN, llevar a cabo una sincronización o recurrir a cualquier otro método o herramienta que use para mover bases de datos de producción.  
  
## <a name="resource-demands-for-tabular-and-multidimensional-workloads"></a>Demandas de recursos en cargas de trabajo tabulares y multidimensionales  
 La siguiente tabla es un resumen de alto nivel de cómo Analysis Services usa los recursos del sistema en las consultas y el procesamiento, distinguiendo entre almacenamiento y modo de servidor. Gracias a este resumen, sabrá en qué centrarse en una implementación multiservidor responsable de una carga de trabajo distribuida.  
  
|||  
|-|-|  
|**Modo de almacenamiento y servidor**|**Impacto en los recursos del sistema**|  
|Tabular en memoria (predeterminado) donde las consultas se ejecutan como recorridos de tabla de estructuras de datos en memoria.|Céntrese en la RAM y las CPU con velocidades de reloj rápidas.|  
|Tabular en modo DirectQuery, donde las consultas se descargan en servidores de bases de datos relacionales back-end y el procesamiento se limita a construir los metadatos del modelo.|Céntrese en el rendimiento de las bases de datos relacionales, en reducir la latencia de la red y en maximizar el rendimiento. Unas CPU más rápidas contribuyen a mejorar el rendimiento del procesador de consultas de Analysis Services.|  
|Modelos multidimensionales que usan almacenamiento MOLAP|Elija una configuración equilibrada que dé cabida a E/S de disco para cargar datos rápidamente y a suficiente RAM para almacenar datos en caché.|  
|Modelos multidimensionales que usan almacenamiento ROLAP|Maximice la E/S de disco y minimice la latencia de red.|  
  
## <a name="highly-availability-and-redundancy-through-wsfc"></a>Alta disponibilidad y redundancia a través de WSFC  
 Analysis Services se puede instalar en un clúster de conmutación por error de Windows (WSFC) existente para lograr una disponibilidad elevada que permita restaurar el servicio en el menor tiempo posible.  
  
 Los clústeres de conmutación por error proporcionan pleno acceso (de lectura y de escritura diferida) a la base de datos, pero solo de nodo a nodo. Las bases de datos secundarias se ejecutan en otros nodos del clúster a modo de servidores de reemplazo si el primer nodo deja de funcionar.  
  
 La principal ventaja de los clústeres de conmutación por error es que permiten recuperarse rápidamente de un error del servicio. Pero esta ventaja conlleva ciertas limitaciones. En primer lugar, si nunca se necesita la conmutación por error, los recursos dedicados en el clúster estarán inactivos. En segundo lugar, si se produce una conmutación por error, todas las conexiones se perderán, con la consiguiente pérdida de trabajo no confirmado. La mayoría de las aplicaciones cliente deben ser capaces de abordar esta situación; a menudo, se puede utilizar el botón Actualizar de la aplicación para recuperar los resultados. 
 
 En lo que respecta a WSFC, tenga en cuenta los puntos siguientes:

- Actualmente no se admite el modo activo/activo. El modo activo/pasivo (conmutación por error) es la única configuración de WSFC admitida para Analysis Services.
- Al implementar Analysis Services en un clúster, asegúrese de que los nodos que participan en el clúster se ejecuten en hardware idéntico o muy similar y que el contexto operativo de cada nodo sea el mismo en lo que respecta a la versión del sistema operativo y los Service Pack, la versión de Analysis Services y los Service Pack (o actualizaciones acumulativas) y el modo de servidor.
- Evite reasignar un nodo pasivo como nodo activo de otra carga de trabajo. Si el nodo no puede controlar las cargas de trabajo, se perderán las ganancias a corto plazo en el uso del equipo en caso de una situación real de conmutación por error.
 
 En estas notas del producto encontrará instrucciones detalladas e información general sobre la implementación de Analysis Services en un clúster de conmutación por error: [How to Cluster SQL Server Analysis Services](https://msdn.microsoft.com/library/dn736073.aspx)(Cómo implementar SQL Server Analysis Services en un clúster). Aunque redactado para SQL Server 2012, este documento sigue siendo válido para las versiones más recientes de Analysis Services.  
  
## <a name="see-also"></a>Vea también  
 [Sincronizar bases de datos de Analysis Services](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)   
 [Forzar la afinidad NUMA para bases de datos tabulares de Analysis Services](https://blogs.msdn.microsoft.com/sqlcat/2013/11/05/forcing-numa-node-affinity-for-analysis-services-tabular-databases/)   
 [Un caso práctico de Analysis Services: Uso de modelos tabulares en una solución comercial a gran escala](https://msdn.microsoft.com/library/dn751533.aspx)  
  
  
