---
title: "Procedimientos recomendados para la administración de replicación | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- administering replication, best practices
- replication [SQL Server], administering
ms.assetid: 850e8a87-b34c-4934-afb5-a1104f118ba8
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 8095467cab3e2548db2afd626190b27b1f5a824f
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2018
---
# <a name="best-practices-for-replication-administration"></a>Prácticas recomendadas para la administración de replicación
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Después de configurar la replicación, es importante entender cómo administrar una topología de replicación. En este tema se proporciona una guía básica de prácticas recomendadas en varias áreas con vínculos a más información de cada área. Además de seguir la guía de procedimientos recomendados que se presenta en este tema, puede leer el tema de preguntas más frecuentes para familiarizarse con preguntas y problemas comunes: [Preguntas más frecuentes para administradores de replicación](../../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md).  
  
 Es útil dividir la guía de prácticas recomendadas en dos áreas:  
  
-   La siguiente información cubre las prácticas recomendadas que se deben implementar para todas las topologías de replicación:  
  
    -   Desarrollar y probar una estrategia de copias de seguridad y restauración  
  
    -   Generar script de la topología de replicación  
  
    -   Crear umbrales y alertas  
  
    -   Supervisar la topología de replicación  
  
    -   Establecer líneas de base de rendimiento y optimizar la replicación si es necesario  
  
-   La siguiente información cubre las prácticas recomendadas que deben tenerse en cuenta pero que pueden no ser necesarias para su topología:  
  
    -   Validar los datos periódicamente  
  
    -   Ajustar los parámetros de agentes mediante perfiles  
  
    -   Ajustar los períodos de retención de publicación y distribución  
  
    -   Conocer cómo cambiar las propiedades de artículos y publicaciones si cambian los requisitos de la aplicación  
  
    -   Conocer cómo realizar cambios de esquema si cambian los requisitos de la aplicación  
  
## <a name="develop-and-test-a-backup-and-restore-strategy"></a>Desarrollar y probar una estrategia de copias de seguridad y restauración  
 Se debe hacer una copia de seguridad de todas las bases de datos regularmente, y se debe comprobar periódicamente la posibilidad de restaurar dichas copias de seguridad; esto es igualmente aplicable a las bases de datos replicadas. Debe realizarse una copia de seguridad de las siguientes bases de datos regularmente.  
  
-   Base de datos de publicaciones  
  
-   Base de datos de distribución  
  
-   Bases de datos de suscripciones  
  
-   Base de datos**msdb** y base de datos **master** en el publicador, distribuidor y todos los suscriptores  
  
 Las bases de datos replicadas requieren una atención especial en relación con la copia de seguridad y restauración de los datos. Para obtener más información, vea [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md).  
  
## <a name="script-the-replication-topology"></a>Generar script de la topología de replicación  
 Todos los componentes de replicación de una topología deben convertirse en script como parte de un plan de recuperación de desastres y, además, los scripts también pueden utilizarse para automatizar tareas repetitivas. Un script contiene los procedimientos almacenados del sistema [!INCLUDE[tsql](../../../includes/tsql-md.md)] necesarios para implementar los componentes de replicación incluidos en los scripts, tales como una publicación o suscripción. Los scripts se pueden crear en un asistente (como el Asistente para nueva publicación) o en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] después de crear un componente. Puede ver, modificar y ejecutar el script mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o **sqlcmd**. Los scripts se pueden almacenar con los archivos de copia de seguridad para utilizarlas en el caso de que se deba volver a configurar una topología de replicación. Para más información, consulte [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
 Se debe volver a crear el script de un componente si se realiza cualquier cambio en las propiedades. Si utiliza procedimientos almacenados personalizados con la replicación transaccional, debe guardar una copia de cada procedimiento con los scripts; la copia se debe actualizar si el procedimiento cambia (los procedimientos se actualizan normalmente como consecuencia de cambios de esquema o cambios en los requisitos de la aplicación. Para obtener más información sobre los procedimientos personalizados, vea [Especificar cómo se propagan los cambios para los artículos transaccionales](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
## <a name="establish-performance-baselines-and-tune-replication-if-necessary"></a>Establecer líneas de base de rendimiento y optimizar la replicación si es necesario  
 Antes de configurar la replicación, se recomienda que se familiarice con los factores que afectan al rendimiento de la replicación:  
  
-   Hardware de servidor y red  
  
-   Diseño de la base de datos  
  
-   Configuración del distribuidor  
  
-   Diseño y opciones de publicación  
  
-   Diseño y uso de los filtros  
  
-   Opciones de suscripción  
  
-   Opciones de instantáneas  
  
-   Parámetros de agente  
  
-   Mantenimiento  
  
 Después de configurar la replicación, se recomienda desarrollar una línea de base de rendimiento que le permita determinar cómo se comporta la replicación con una carga de trabajo que sea habitual para sus aplicaciones y topología. Utilice el Monitor de replicación y el Monitor de sistema para determinar los valores típicos de las cinco dimensiones siguientes del rendimiento de la replicación:  
  
-   Latencia: la cantidad de tiempo que se tarda en propagar un cambio de datos entre nodos en una topología de replicación.  
  
-   Rendimiento: la cantidad de actividad de replicación (medida en comandos suministrados durante un período de tiempo) que un sistema puede mantener en el tiempo.  
  
-   Simultaneidad: el número de procesos de replicación que pueden operar simultáneamente en un sistema.  
  
-   Duración de sincronización: el tiempo que tarda en finalizar una sincronización determinada  
  
-   Utilización de recursos: recursos de hardware y de red utilizados como resultado del procesamiento de replicación.  
  
 La latencia y el rendimiento son las más relevantes para la replicación transaccional, porque los sistemas basados en la replicación transaccional requieren generalmente latencia baja y alto rendimiento. La simultaneidad y la duración de sincronización son las más relevantes para la replicación de mezcla, porque los sistemas basados en la replicación de mezcla suelen tener un gran número de suscriptores, y un publicador puede tener un número significativo de sincronizaciones simultáneas con estos suscriptores.  
  
 Después de que haya establecido números de línea de base, establezca umbrales en el Monitor de replicación. Para obtener más información, vea [Establecer umbrales y advertencias en el Monitor de replicación](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md) y [Usar alertas para eventos del Agente de replicación](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md). Si se encuentra con un problema de rendimiento, se recomienda leer las sugerencias de los temas para mejorar el rendimiento enumerados anteriormente y aplicar cambios en áreas que afecten a los problemas que ha encontrado.  
  
## <a name="create-thresholds-and-alerts"></a>Crear umbrales y alertas  
 El Monitor de replicación le permite establecer un número de umbrales relacionados con el estado y el rendimiento. Se recomienda establecer los umbrales apropiados para su topología; si se alcanza un umbral, se mostrará una advertencia y, opcionalmente, se puede enviar una alerta a una cuenta de correo electrónico, un buscapersonas u otro dispositivo. Para más información, consulte [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
 Además de las alertas que se pueden asociar con los umbrales de supervisión, la replicación ofrece un número de alertas predefinidas que responden a las acciones del agente de replicación. Un administrador puede utilizar estas alertas para mantenerse informado sobre el estado de la topología de replicación. Se recomienda leer el tema en el que se describen las alertas y utilizar aquellas que se adapten a las necesidades de administración (también es posible crear alertas adicionales si es necesario). Para obtener más información, vea [Usar alertas para eventos del Agente de replicación](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md).  
  
## <a name="monitor-the-replication-topology"></a>Supervisar la topología de replicación  
 Después de aplicar la topología de replicación y configurar los umbrales y alertas, se recomienda supervisar la replicación regularmente. Supervisar una topología de replicación es un aspecto importante en la implementación de la replicación. Debido a que la actividad de replicación se distribuye, es fundamental realizar un seguimiento de la actividad y el estado de todos los equipos que participan en la replicación. Para supervisar la replicación se pueden utilizar las siguientes herramientas:  
  
-   El Monitor de replicación es la herramienta más importante para la supervisión de la replicación, ya que le permite supervisar el estado general de una topología de replicación. Para más información, consulte [Monitoring Replication](../../../relational-databases/replication/monitor/monitoring-replication-overview.md).  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)] y Replication Management Objects (RMO) proporcionan interfaces para supervisar la replicación. Para más información, consulte [Monitoring Replication](../../../relational-databases/replication/monitor/monitoring-replication-overview.md).  
  
-   El Monitor de sistema también puede ser útil para supervisar el rendimiento de la replicación. Para más información, consulte [Monitoring Replication with System Monitor](../../../relational-databases/replication/monitor/monitoring-replication-with-system-monitor.md).  
  
## <a name="validate-data-periodically"></a>Validar los datos periódicamente  
 La replicación no requiere validación, pero se recomienda ejecutar la validación periódicamente en la replicación transaccional y la replicación de mezcla. La validación le permite comprobar que los datos del suscriptor coinciden con los datos del publicador. Una validación satisfactoria indica que en ese momento se han replicado todos los cambios del publicador en el suscriptor (y del suscriptor en el publicador si el suscriptor admite actualizaciones) y que las dos bases de datos están sincronizadas.  
  
 Se recomienda realizar la validación de acuerdo con la programación de copia de seguridad de la base de datos de publicaciones. Por ejemplo, si se realiza una copia de seguridad completa de la base de datos de publicaciones una vez a la semana, se podría ejecutar la validación una vez a la semana tras finalizar la copia de seguridad. Para obtener más información, vea [Validar datos replicados](../../../relational-databases/replication/validate-replicated-data.md).  
  
## <a name="use-agent-profiles-to-change-agent-parameters-if-necessary"></a>Utilizar perfiles para cambiar los parámetros de agentes si es necesario  
 Los perfiles de agente proporcionan un método cómodo para establecer los parámetros de los agentes de replicación. También se pueden especificar los parámetros en la línea de comandos del agente, pero normalmente es más apropiado utilizar un perfil de agente predefinido o crear un perfil nuevo si necesita cambiar el valor de un parámetro. Por ejemplo, si está utilizando la replicación de mezcla y un suscriptor pasa de una conexión de banda ancha a una conexión telefónica, considere la posibilidad de utilizar el perfil **slow link** para el Agente de mezcla; este perfil utiliza un conjunto de parámetros que se ajustan mejor al vínculo de comunicaciones más lento. Para obtener más información, consulte [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
## <a name="adjust-publication-and-distribution-retention-periods-if-necessary"></a>Ajustar los períodos de retención de publicación y distribución si es necesario  
 La replicación transaccional y la replicación de mezcla utilizan períodos de retención para determinar, respectivamente, cuánto tiempo se almacenan las transacciones en la base de datos de distribución y la frecuencia con que se debe sincronizar una suscripción. Se recomienda utilizar la configuración predeterminada inicialmente, pero supervisar la topología para determinar si la configuración necesita ajustes. Por ejemplo, en el caso de la replicación de mezcla, el período de retención de publicación (que es de 14 días de manera predeterminada) determina cuánto tiempo se almacenan los metadatos en las tablas del sistema. Si las suscripciones se sincronizan siempre en un plazo de cinco días, considere el ajuste de la configuración a un número inferior, que reducirá los metadatos y posiblemente proporcionará un mejor rendimiento. Para más información, consulte [Subscription Expiration and Deactivation](../../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
## <a name="understand-how-to-modify-publications-if-application-requirements-change"></a>Conocer cómo modificar las publicaciones si cambian los requisitos de la aplicación  
 Una vez creada una publicación, puede ser necesario agregar o quitar artículos, o cambiar las propiedades de la publicación o de un artículo. Es posible realizar la mayoría de los cambios una vez creada la publicación. Sin embargo, en algunos casos, es necesario generar una nueva instantánea de la publicación o reinicializar las suscripciones de la misma. Para más información, vea [Change Publication and Article Properties](../../../relational-databases/replication/publish/change-publication-and-article-properties.md) (Cambiar las propiedades de la publicación y de los artículos) y [Agregar y quitar artículos de publicaciones existentes](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
## <a name="understand-how-to-make-schema-changes-if-application-requirements-change"></a>Conocer cómo realizar cambios de esquema si cambian los requisitos de la aplicación  
 En muchos casos, son necesarios cambios de esquema después de que una aplicación esté en producción. En una topología de replicación, a menudo se deben propagar estos cambios a todos los suscriptores. La replicación admite una gran variedad de cambios en el esquema de objetos publicados. Cuando se realiza cualquiera de los siguientes cambios de esquema en el objeto publicado apropiado en un publicador de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , dicho cambio se propaga de manera predeterminada a todos los suscriptores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
-   ALTER TABLE  
  
-   ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
 Para obtener más información, vea [Make Schema Changes on Publication Databases](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md) (Realizar cambios de esquema en bases de datos de publicaciones).  
  
## <a name="see-also"></a>Ver también  
 [Administración &#40;replicación&#41;](../../../relational-databases/replication/administration/administration-replication.md)  
  
  
