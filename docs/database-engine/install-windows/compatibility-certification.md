---
title: Certificación de compatibilidad | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], databases
- compatibility levels [SQL Server], after upgrade
- Database Engine [SQL Server], upgrading
- Databases [SQL Server], upgrading
- Database Engine [SQL Server], upgrading
- compatibility [SQL Server], certification
- compatibility level [SQL Server], upgrades
ms.assetid: 3c036813-36cf-4415-a0c9-248d0a433856
author: pmasl
ms.author: pelopes
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: bc4ed369b51187a86e9436e6612522d6707a3d54
ms.sourcegitcommit: 445842da7c7d216b94a9576e382164c67f54e19a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/30/2019
ms.locfileid: "71682044"
---
# <a name="compatibility-certification"></a>Certificación de compatibilidad

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

La certificación de compatibilidad permite que las empresas actualicen y modernicen una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el entorno local, en la nube y en el perímetro, lo cual elimina los riesgos relativos a la compatibilidad de las aplicaciones. 

El mismo [!INCLUDE[ssde_md](../../includes/ssde_md.md)] activa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)], incluida la Instancia administrada. Este recurso compartido [!INCLUDE[ssde_md](../../includes/ssde_md.md)] significa que una base de datos de usuario puede moverse sin problemas entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el entorno local y [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)], mientras que el código de aplicación que se ejecuta en la base de datos como [!INCLUDE[tsql](../../includes/tsql-md.md)] sigue funcionando como en su sistema de origen.

En cada versión nueva de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el nivel de compatibilidad predeterminado se establece en la versión de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Sin embargo, el nivel de compatibilidad de las versiones anteriores se conserva para mantener la compatibilidad continua de las aplicaciones existentes. Esta matriz de compatibilidad se puede ver [aquí](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#supported-dbcompats).
Por lo tanto, una aplicación que estuviera certificada para trabajar con una versión determinada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en realidad estaba certificada para funcionar en el nivel de compatibilidad predeterminado de esa versión.

Por ejemplo, el nivel de compatibilidad de la base de datos 130 era el valor predeterminado en [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Dado que los niveles de compatibilidad fuerzan determinados comportamientos funcionales y de optimización de consultas de [!INCLUDE[tsql](../../includes/tsql-md.md)], una base de datos certificada para funcionar en [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] se ha certificado implícitamente en el nivel de compatibilidad 130 de la base de datos. Esta base de datos puede funcionar tal cual en una versión más reciente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (como [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) y [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)], siempre que el nivel de compatibilidad de la base de datos se mantenga en 130. 

Este es un principio fundamental para el modelo de operación de integración continua de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]. El [!INCLUDE[ssde_md](../../includes/ssde_md.md)] se mejora y actualiza continuamente en Azure, pero dado que las bases de datos existentes mantienen su nivel de compatibilidad actual, estas continúan funcionando como se han diseñado incluso después de las actualizaciones al [!INCLUDE[ssde_md](../../includes/ssde_md.md)]subyacente. 

## <a name="managing-upgrade-risk-with-compatibility-certification"></a>Administración del riesgo de actualización con la certificación de compatibilidad
El uso de la certificación de compatibilidad es un enfoque valioso para la modernización de las bases de datos. Mediante la certificación basada en el nivel de compatibilidad, los desarrolladores establecen los requisitos técnicos para que una aplicación se admita en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)], pero desacoplan el ciclo de vida de la aplicación del de la plataforma de las bases de datos. Esto permite a las empresas mantener el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] actualizado según sea necesario de acuerdo con las directivas del ciclo de vida, así como aprovechar las nuevas mejoras de escalabilidad y rendimiento que no dependen del código y conectar aplicaciones para **mantener su estado funcional** a través de actualizaciones.

La posibilidad de afectar negativamente a la funcionalidad y el rendimiento son los principales factores de riesgo de cualquier actualización. La certificación de compatibilidad representa una tranquilidad en cuanto a la administración de estos riesgos de actualización:

-  En lo que se refiere al comportamiento de [!INCLUDE[tsql](../../includes/tsql-md.md)], cualquier cambio significa que una aplicación debe volver a certificarse para que sea correcta. Sin embargo, la configuración del [nivel de compatibilidad de la base de datos](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md) proporciona compatibilidad con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo para la base de datos especificada, no para todo el servidor. Mantener el nivel de compatibilidad de la base de datos tal y como está garantiza que las consultas de las aplicaciones existentes sigan mostrando el mismo comportamiento antes y después de una actualización de [!INCLUDE[ssde_md](../../includes/ssde_md.md)]. Para obtener más información sobre los niveles de compatibilidad y comportamiento de [!INCLUDE[tsql](../../includes/tsql-md.md)], consulte [Usar el nivel de compatibilidad para la compatibilidad con versiones anteriores](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#using-compatibility-level-for-backward-compatibility).

-  En lo que se refiere al rendimiento, dado que las mejoras en el optimizador de consultas se introducen con cada versión, se podrían esperar diferencias en los planes de consulta entre distintas versiones de [!INCLUDE[ssde_md](../../includes/ssde_md.md)]. Las diferencias de los planes de consulta en el ámbito de una actualización normalmente se traducen en un riesgo cuando es posible que algunos cambios puedan ser perjudiciales para determinada consulta o carga de trabajo. A su vez, este riesgo es una motivación para la recertificación, que puede retrasar las actualizaciones y plantear problemas relativos al ciclo de vida y el soporte técnico. 
   La mitigación de los riesgos de actualización es el motivo por el que las mejoras del optimizador de consultas se canalizan en el nivel de compatibilidad predeterminado de una nueva versión. La certificación de compatibilidad incluye la **protección de las formas de los planes de consulta**: el principio de mantener el nivel de compatibilidad de la base de datos tal cual inmediatamente después de una actualización de [!INCLUDE[ssde_md](../../includes/ssde_md.md)] significa que el modelo de optimización de consultas usado para crear planes de consulta en la nueva versión es el mismo que antes de la actualización y que la forma del plan de consulta no debe cambiar. 
   
   > [!NOTE]
   > **La forma del plan de consulta** hace referencia a la representación visual de los distintos operadores que componen un plan de consulta. Esto incluye operadores como búsquedas, exámenes, combinaciones y ordenaciones, así como las conexiones entre ellos que indican el flujo de datos y el orden de las operaciones. El optimizador de consultas determina la forma del plan de consulta. Para más información, vea la [Guía de arquitectura de procesamiento de consulta](../../relational-databases/query-processing-architecture-guide.md#optimizing-select-statements).
   
   Para más información, vea [Uso de niveles de compatibilidad para la compatibilidad con versiones anteriores](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#using-compatibility-level-for-backward-compatibility).
   
Siempre y cuando la aplicación no necesite aprovechar las mejoras que solo están disponibles en un nivel de compatibilidad de base de datos superior, es un enfoque válido para actualizar el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y mantener el nivel de compatibilidad de base de datos anterior, sin necesidad de volver a certificar una aplicación. Para obtener más información, consulte [Actualizaciones del motor de base de datos y niveles de compatibilidad](#compatibility-levels-and-database-engine-upgrades), más adelante en este artículo.

Para los nuevos trabajos de desarrollo, o en el caso de que una aplicación existente requiera el uso de características nuevas, como el [Procesamiento de consultas inteligentes](../../relational-databases/performance/intelligent-query-processing.md), así como algunos [!INCLUDE[tsql](../../includes/tsql-md.md)] nuevos, plantéese actualizar el nivel de compatibilidad de base de datos a la versión más reciente disponible en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y certifique la aplicación para que funcione con ese nivel de compatibilidad. Para obtener más información detallada sobre cómo actualizar el nivel de compatibilidad de base de datos, vea [Prácticas recomendadas para actualizar el nivel de compatibilidad de base de datos](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#best-practices-for-upgrading-database-compatibility-level).

## <a name="compatibility-certification-benefits"></a>Ventajas de la certificación de compatibilidad
El uso de la certificación de bases de datos como enfoque basado en la compatibilidad, en lugar de un enfoque de versión con nombre, ofrece varias ventajas inmediatas:

-  **Desacople la certificación de la aplicación de la plataforma**. Debido a su recurso compartido [!INCLUDE[ssde_md](../../includes/ssde_md.md)], en el caso de las aplicaciones que solo necesitan ejecutar consultas de [!INCLUDE[tsql](../../includes/tsql-md.md)], no es necesario mantener procesos de certificación independientes para Azure y el entorno local.
-  **Reduzca los riesgos de las actualizaciones**, ya que, durante la modernización de la plataforma de las bases de datos, los ciclos de actualización del nivel de plataforma de las bases datos y la aplicación pueden separarse con menos interrupciones y una administración de cambios mejorada.
-  **Realice actualizaciones sin cambios en el código**. La actualización a una nueva versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] puede realizarse sin cambios en el código, manteniendo el mismo nivel de compatibilidad que el sistema de origen y sin la necesidad inmediata de volver a realizar la certificación hasta que la aplicación necesite sacar provecho de las mejoras que solo estén disponibles en niveles de compatibilidad superiores de las bases de datos.
- **Mejore la capacidad de administración y escalabilidad** sin necesidad de realizar cambios en la aplicación, con mejoras que no se canalicen mediante el nivel de compatibilidad de la base de datos. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se incluyen, por ejemplo: 
  - Una supervisión enriquecida y mejoras en la solución de problemas, con nuevas [vistas de administración dinámica del sistema](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md), [eventos extendidos](../../relational-databases/extended-events/extended-events.md) y [ajuste automático](../../relational-databases/automatic-tuning/automatic-tuning.md). 
  - Escalabilidad mejorada con [soft-NUMA automático](../../database-engine/configure-windows/soft-numa-sql-server.md#automatic-soft-numa).

Las nuevas bases de datos todavía se establecen en el nivel de compatibilidad predeterminado de la versión de [!INCLUDE[ssde_md](../../includes/ssde_md.md)]. Sin embargo, cuando se mueve una base de datos de una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a una nueva versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)], la base de datos mantiene su nivel de compatibilidad existente. 

> [!IMPORTANT]
> Antes de mover una base de datos a una nueva versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)], compruebe si todavía se admite el nivel de compatibilidad de la base de datos. La matriz de compatibilidad del nivel de compatibilidad de la base de datos se puede ver [aquí](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#arguments). 
>
> Actualizar una base de datos con un nivel de compatibilidad inferior al nivel permitido (por ejemplo, 90, que era el valor predeterminado en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]) hace que la base de datos se establezca automáticamente en el nivel de compatibilidad más bajo permitido (100).
>
> Para averiguar el nivel de compatibilidad actual, consulte la columna **compatibility_level** de [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).

## <a name="compatibility-levels-and-database-engine-upgrades"></a>Actualizaciones del motor de base de datos y niveles de compatibilidad
Para actualizar [!INCLUDE[ssde_md](../../includes/ssde_md.md)] a la versión más reciente y mantener al mismo tiempo el nivel de compatibilidad de base de datos que existía antes de la actualización y su estado de compatibilidad, se recomienda realizar la validación del área de superficie funcional estática del código de aplicación de la base de datos (objetos de programación, como procedimientos almacenados, funciones, desencadenadores y demás) y de la aplicación (mediante un seguimiento de la carga de trabajo que captura el código dinámico enviado por la aplicación), mediante la herramienta [Microsoft Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA). La ausencia de errores en la salida de la herramienta DMA, sobre funcionalidades incompatibles o ausentes, protege la aplicación de cualquier regresión funcional en la nueva versión de destino. Para obtener más información, vea [Información general de Data Migration Assistant](../../dma/dma-overview.md).

> [!NOTE]
> DMA admite el nivel de compatibilidad de base de datos 100 y posterior. Queda excluido [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] como versión de origen.   

> [!IMPORTANT]
> [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que se lleven a cabo algunas pruebas mínimas para validar el éxito de una actualización, mientras se mantiene el nivel de compatibilidad de base de datos anterior. Debe determinar qué comprenderían estas pruebas mínimas para su aplicación y su escenario.   

> [!NOTE]
> [!INCLUDE[msCoName](../../includes/msconame-md.md)] ofrece protección de formas de los planes de consulta cuando:
>
> - La nueva versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (destino) se ejecuta en un hardware comparable al hardware en el que se ejecutaba la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anterior (origen).
> - Se usa el mismo [nivel de compatibilidad de base de datos admitido](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#supported-dbcompats) tanto en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino como en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de origen.
>
> Se corregirán todas las regresiones de forma de los planes de consulta (en comparación con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de origen) que se produzcan en las condiciones anteriores. Póngase en contacto con el servicio de atención al cliente de Microsoft si es el caso.
  
## <a name="see-also"></a>Consulte también 
[Nivel de compatibilidad de ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)       
[Ver o cambiar el nivel de compatibilidad de una base de datos](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)       
[Prácticas recomendadas para actualizar el nivel de compatibilidad de base de datos](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#best-practices-for-upgrading-database-compatibility-level)      
