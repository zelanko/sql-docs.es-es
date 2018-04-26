---
title: Conceptos de la programación de replicación | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- replication [SQL Server], planning
- programming [SQL Server replication], planning
- programming [SQL Server replication]
ms.assetid: 2cd846e7-5bf3-4144-8772-703c4f439a2a
caps.latest.revision: 43
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 03c7bf1b7fca64d18bb01732c7f98f6f106ec849
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="replication-programming-concepts"></a>Conceptos de la programación de replicación
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Antes de desarrollar una aplicación que utilice funcionalidades de replicación, debería seguir los pasos de planeamiento generales siguientes:  
  
1.  Definir la topología de replicación.  
  
2.  Definir la funcionalidad de la aplicación.  
  
3.  Planear la seguridad.  
  
4.  Elegir un entorno de desarrollo.  
  
5.  Elegir la interfaz de programación de la replicación adecuada.  
  
 El resto de este tema describe estos pasos con más detalle. Para ayudar a mostrar el proceso de planeamiento, se ha incluido un ejemplo.  
  
## <a name="defining-the-replication-topology"></a>Definir la topología de replicación  
 El primer paso para programar la replicación es definir la topología de replicación de la aplicación. Si está creando una aplicación que vaya a usar una topología de replicación existente, por ejemplo una aplicación cliente que tiene acceso a los datos de un suscriptor existente, debería continuar en el paso siguiente.  
  
> [!NOTE]  
>  En algunos casos, implementar la topología de replicación será la única finalidad de la aplicación.  
  
 La topología de replicación que defina depende de muchos factores, como son los siguientes:  
  
-   Si los datos replicados tienen que estar actualizados y quién debe actualizarlos.  
  
-   Las necesidades de distribución de los datos con respecto a la coherencia, autonomía y latencia.  
  
-   El entorno de replicación, incluidos los usuarios empresariales, la infraestructura técnica, la red y la seguridad, y las características de los datos.  
  
-   Los tipos y las opciones de replicación.  
  
-   Las topologías de replicación y cómo se alinean con los tipos de replicación.  
  
 Si carece de experiencia con la replicación de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vea [Tipos de replicación](../../../relational-databases/replication/types-of-replication.md).  
  
## <a name="defining-application-functionality"></a>Definir la funcionalidad de la aplicación  
 Una vez definida la topología de replicación, debería decidir las funcionalidades que la aplicación proporcionará. Estas funcionalidades pueden abarcar desde un script que sincronice una suscripción a una aplicación con una interfaz de usuario para configurar la replicación. La replicación admite las tareas generales de programación siguientes:  
  
-   Configurar la replicación.  
  
-   Sincronizar suscripciones.  
  
-   Mantener una topología de replicación.  
  
-   Supervisar una topología de replicación.  
  
-   Solucionar problemas de la replicación.  
  
 También es común ampliar la aplicación combinando las funcionalidades de replicación con otras funcionalidades que se proporcionan a través de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. En la tabla siguiente se resaltan algunas funcionalidades extendidas que podría proporcionar en la aplicación de replicación.  
  
|Funcionalidad|Ejemplo|  
|-------------------|-------------|  
|Administración de servidor con Objetos de administración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)](SMO)|Una aplicación que permite que un administrador adjunte y configure una base de datos como publicador en una topología de replicación.|  
|Acceso a datos con ADO.NET|Una aplicación que permite que los usuarios obtengan acceso mediante programación y cambien los datos de ventas replicados en una base de datos de suscriptor local mientras está sin conexión y, a continuación, conecten y sincronicen la suscripción de extracción haciendo clic en un botón.|  
  
## <a name="planning-for-security"></a>Planear la seguridad  
 La seguridad es importante en cualquier aplicación y su planeamiento se debería completar antes de escribir ningún código. La seguridad de la aplicación puede dividirse en tres partes principales: proteger la base de datos, proteger la replicación y escribir código seguro.  
  
 Los siguientes temas proporcionan información sobre la seguridad:  
  
-   [Seguridad y protección &#40;Replicación&#41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
-   [Centro de seguridad para el motor de base de datos SQL Server y la base de datos SQL Azure](../../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
## <a name="choosing-a-development-environment"></a>Elegir un entorno de desarrollo  
 Al desarrollar una aplicación de replicación, hay que considerar tres entornos de desarrollo básicos. Cada uno tiene acceso a las mismas funcionalidades de replicación con algunas excepciones. Las aplicaciones de replicación se pueden desarrollar en cada uno de los entornos siguientes.  
  
-   **Código administrado**  
  
     Entorno de desarrollo orientado a objetos que aprovecha las ventajas de la programación de [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] y Common Language Runtime (CLR) de .NET. El código administrado es el entorno de programación recomendado para el desarrollo de .NET y para las aplicaciones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Las interfaces de replicación administradas habilitan la programación de la administración de la replicación de una manera orientada a objetos sin tener que conocer [!INCLUDE[tsql](../../../includes/tsql-md.md)] y también proporcionan algunas funcionalidades de devolución de llamada al ejecutar agentes de replicación que no están disponibles en los scripts. El código administrado es el mejor entorno para desarrollar componentes reutilizables y aplicaciones de interfaz de usuario.  
  
-   **Scripting**  
  
     Aplicaciones sencillas que ejecutan una serie de comandos como procedimientos almacenados del sistema de replicación en scripts o comandos de [!INCLUDE[tsql](../../../includes/tsql-md.md)] en archivos por lotes. Aunque puede ejecutar los scripts en un entorno administrado utilizando el proveedor administrado en proceso de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], la misma funcionalidad se puede obtener mediante interfaces de replicación administradas, que también proporcionan funcionalidades de devolución de llamada. El scripting es el mejor entorno para ejecutar tareas que se ejecutarán solo algunas veces y en las que no se requieren las funcionalidades de devolución de llamada, como instalar un servidor de replicación.  
  
-   **Código nativo**  
  
     El CLR no administra el entorno de desarrollo orientado a objetos que utiliza el acceso directo al sistema o a los objetos COM como ese código. Las interfaces de replicación de código nativo han quedado obsoletas o han dejado de utilizarse. Para obtener más información, vea [Características que ya no se usan en la replicación de SQL Server](../../../relational-databases/replication/deprecated-features-in-sql-server-replication.md) o [Compatibilidad con versiones anteriores de replicación](../../../relational-databases/replication/replication-backward-compatibility.md).  
  
## <a name="choose-the-appropriate-replication-programming-interface"></a>Elegir la interfaz de programación de replicación adecuada  
 El último paso del planeamiento es elegir la interfaz de programación de la replicación adecuada que implementa la funcionalidad de replicación deseada para el entorno de desarrollo elegido. En la tabla siguiente se muestran las interfaces de programación de la replicación disponible.  
  
|Interfaz|Entorno|Usos|  
|---------------|-----------------|----------|  
|[Replication Management Objects Concepts](../../../relational-databases/replication/concepts/replication-management-objects-concepts.md) (Conceptos de Replication Management Objects)|Código administrado|Administración, supervisión y sincronización.|  
|<xref:Microsoft.SqlServer.Replication>|Código administrado|Sincronización.|  
|<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>|Código administrado|Creación de controladores de lógica de negocios para integrar la lógica personalizada con el proceso de sincronización de mezcla.|  
|[Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)|Scripting|Administración y supervisión.|  
|[Replication Agent Executables Concepts](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)|Scripting|Sincronización.|  
  
## <a name="example"></a>Ejemplo  
 En [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)], tienen que publicarse los datos de 200 representantes de ventas de todo el mundo. Los representantes de ventas viajan a menudo y necesitan utilizar equipos portátiles o asistentes digitales personales (PDA) para cambiar los datos de los clientes y agregar los pedidos nuevos. A continuación, los cambios tendrán que sincronizarse con el publicador cuando el representante de ventas conecte el portátil a la red.  
  
 Para esta aplicación, los pasos de planeamiento podrían ser similares a los siguientes:  
  
1.  La topología de replicación de esta aplicación ya existe. Sin embargo, debe crearse una suscripción de extracción nueva en el cliente. La publicación debería utilizar filtros parametrizados para replicar un conjunto único de datos para cada representante de ventas.  
  
2.  Además del acceso a datos típico requerido para una aplicación de ventas, esta aplicación debería permitir que un vendedor sincronizara la suscripción de extracción a petición haciendo clic en un botón. Puesto que un representante de ventas instalará y ejecutará la aplicación, también necesita poder configurar una suscripción y aplicar la instantánea inicial en el cliente. Opcionalmente, la aplicación utilizará la infraestructura que proporciona Windows para detectar la conectividad inalámbrica y sincronizar automáticamente la suscripción cuando se descubra una conexión.  
  
3.  Siga todas las instrucciones de seguridad para la replicación, incluido el uso de la autenticación de Windows y una red privada virtual (VPN) al conectarse al publicador. Si está implementando la sincronización web, utilice una conexión de capa de sockets seguros (SSL). Para obtener más información, vea [Configure Web Synchronization](../../../relational-databases/replication/configure-web-synchronization.md) (Configurar la sincronización web).  
  
4.  Para aprovechar las características de [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], la aplicación se desarrolla utilizando un lenguaje de código administrado.  
  
5.  Según estos requisitos, la interfaz administrada de Replication Management Objects (RMO) puede proporcionar toda la funcionalidad de la replicación que se necesita para esta aplicación.  
  
 Este escenario de ejemplo se ha implementado en la aplicación de ejemplo de AdventureWorks, que se puede descargar para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
  
