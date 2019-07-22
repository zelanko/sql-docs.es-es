---
title: Cuadro de diálogo "Propiedades de la publicación" de Replicación de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.pubproperties.agentsecurity.f1
- sql13.rep.newpubwizard.pubproperties.agentsecurity.f1
- sql13.rep.newpubwizard.pubproperties.filterrows.f1
- sql13.rep.newpubwizard.pubproperties.internetsynchronization.f1
- sql13.rep.newpubwizard.pubproperties.general.f1
- sql13.rep.newpubwizard.pubproperties.publicationaccesslist.f1
- sql13.rep.newpubwizard.pubproperties.snapshotformat.f1
helpviewer_keywords:
- Publication Properties dialog box
ms.assetid: 66e845e9-1308-4288-9110-ad2f22f1fc58
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7a7478f259dce1654584e3a9b50b081be0ea07f8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67908076"
---
# <a name="sql-server-replication-publication-properties--dialog-box"></a>Cuadro de diálogo "Propiedades de la publicación" de Replicación de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En esta página se describen las páginas del cuadro de diálogo Propiedades de la publicación. 

## <a name="general"></a>General
 La página **General** del cuadro de diálogo **Propiedades de la publicación** contiene información básica acerca de la publicación, incluido el nombre, la descripción y la directiva de expiración de la suscripción.  
  
### <a name="options"></a>Opciones  
 **Nombre**  
 Nombre de la publicación (solo lectura).  
  
 **Base de datos**  
 Nombre de la base de datos de publicación (solo lectura).  
  
 **Descripción**  
 Descripción de la publicación.  
  
 **Tipo**  
 Tipo de publicación (solo lectura).  
  
 **Expiración de la suscripción**  
 Seleccione una de las opciones para la expiración de la suscripción: **Las suscripciones no expiran nunca** o **Las suscripciones expiran**, con un período de tiempo explícito (**Intervalo**).  
  
 En las publicaciones de instantáneas y transaccionales, [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que acepte la opción predeterminada **Las suscripciones no expiran nunca**.  
  
 En las replicaciones de mezcla, [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que acepte la opción predeterminada **Las suscripciones expiran** y establezca el mínimo valor posible en **Intervalo**. A medida que aumenta el período de expiración de la suscripción, también aumentará la cantidad de datos almacenados, lo que podría afectar al rendimiento. Evalúe la necesidad de desconectar suscriptores o de sincronizarlos durante un período prolongado ante los posibles problemas de rendimiento del almacenamiento y procesamiento de grandes cantidades de metadatos.  
  
 Para más información, consulte [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
 **Nivel de compatibilidad**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores solamente, publicaciones de combinación solamente. Seleccione la versión mínima de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] necesaria para que los suscriptores se sincronicen con esta publicación. Existen diversas reglas asociadas a la determinación del nivel de compatibilidad.  

## <a name="filter-rows"></a>Filtrar filas
  La página **Filtrar filas** del cuadro de diálogo **Propiedades de la publicación** permite realizar operaciones de adición, edición o eliminación:  
  
-   Aplicar filtros de fila estática a artículos de la tabla en publicaciones de instantáneas, transaccionales y de mezcla.   
-   Aplicar filtros de fila con parámetros a artículos de la tabla en publicaciones de combinación.    
-   Utilizar filtros de combinación para ampliar los filtros de los artículos de tablas de mezcla a artículos de tablas relacionadas. Para obtener más información sobre las opciones de filtrado, vea [Filtrar datos publicados](../../relational-databases/replication/publish/filter-published-data.md).  
  
> [!NOTE]  
>  Para agregar, editar o eliminar un filtro, se requiere una nueva instantánea para la publicación y, además, deben reinicializarse todas las suscripciones.  
  
Para obtener el máximo rendimiento de la aplicación y reducir la cantidad de almacenamiento remoto necesario, o para restringir la disponibilidad de ciertos datos a suscriptores específicos, debe publicar los datos necesarios. La publicación puede incluir tablas sin filtrar y tablas filtradas. Por ejemplo, podría incluir la tabla completa sin filtrar de los productos de la empresa y utilizar filtros de fila para proporcionar una tabla filtrada de clientes para un área específica. Si filtra los datos publicados, podrá:  
  
-   Minimizar la cantidad de datos que se envían a través de la red.    
-   Reducir la cantidad de espacio de almacenamiento necesario en el suscriptor.    
-   Personalizar las publicaciones y las aplicaciones en función de los requisitos de cada suscriptor.    
-   Evitar o reducir los conflictos si los suscriptores actualizan datos, ya que pueden enviarse particiones de datos diferentes a varios suscriptores (dos suscriptores distintos no actualizarán los mismos valores de datos).    
-   Evitar la transmisión de datos reservados. Se pueden utilizar filtros de fila y filtros de columna para restringir el acceso de un suscriptor a los datos. Para la replicación de mezcla, existen consideraciones de seguridad que se deben tener en cuenta si utiliza un filtro con parámetros que incluya HOST_NAME(). Para obtener más información, vea la sección sobre cómo filtrar con HOST_NAME() en el tema [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
### <a name="options"></a>Opciones  
 **Tablas filtradas**  
 Este panel se llena con filtros según se agregan a los artículos de la tabla en la publicación. Las tablas con filtros de fila se muestran como nodos de nivel superior en el panel. En las publicaciones de combinación, las tablas cuyo filtro se ha ampliado a filtro de combinación se muestran como nodos secundarios.  
  
 **Agregar**  
 Haga clic en **Agregar** para abrir un cuadro de diálogo que permite filtrar artículos de la tabla. Si hace clic en **Agregar** en una publicación de instantáneas o transaccional, se abre inmediatamente un cuadro de diálogo. Al hacer clic en **Agregar** para una publicación de mezcla se muestran tres opciones: **Agregar filtro**; **Agregar combinación para ampliar el filtro seleccionado**; **Generar filtros automáticamente**.  
  
-   Seleccione **Agregar filtro** para abrir el cuadro de diálogo **Agregar filtro** . Este cuadro de diálogo permite aplicar filtros de fila a un artículo de la tabla. En el cuadro de diálogo **Agregar filtro** , por ejemplo, podría especificar que una tabla con datos de cliente solamente debe contener datos de los clientes franceses cuando se replique a los suscriptores.  
  
-   Seleccione **Agregar combinación para ampliar el filtro seleccionado** para abrir el cuadro de diálogo **Agregar combinación** . El cuadro de diálogo **Agregar combinación** permite ampliar un filtro de filas para que se filtren datos de las tablas relacionadas con la tabla que tiene el filtro de fila. Por ejemplo, si una tabla de clientes se filtra para que solo contenga datos de clientes franceses, y existe una tabla relacionada de pedidos de clientes, puede definir una combinación entre las dos tablas para que la tabla de pedidos solo incluya pedidos de los clientes franceses.  
  
    > [!NOTE]  
    >  Esta opción está disponible solo si primero selecciona la tabla base de la combinación en el panel de filtros.  
  
-   Seleccione **Generar filtros automáticamente** para abrir el cuadro de diálogo **Generar filtros** . Este cuadro de diálogo permite definir un filtro de filas en una tabla en una publicación de combinación que la replicación extiende automáticamente a otras tablas relacionadas a través de relaciones de clave externa. Por ejemplo, una publicación podría incluir tres tablas: una tabla de cliente, una tabla de pedidos (con una clave externa a la tabla de clientes) y una tabla de detalles de pedidos (con una clave externa a la tabla de pedidos). Defina un filtro de filas en la tabla de clientes y la replicación lo extenderá a las otras tablas.  
  
    > [!NOTE]  
    >  Cuando la replicación genera filtros automáticamente, se eliminan los filtros existentes en la publicación. Para incluir los filtros generados automáticamente y los filtros especificados manualmente, primero genere los filtros. Solo puede especificar un conjunto de filtros generados automáticamente en cada publicación.  
  
 **Editar**  
 Seleccione un filtro de filas o un filtro de combinación en el panel de filtros y haga clic en **Editar** para abrir el cuadro de diálogo **Editar filtro** o **Editar combinación** .  
  
 **Eliminar**  
 Seleccione un filtro de filas o un filtro de combinación en el panel de filtros y haga clic en **Eliminar** para eliminar el filtro.  
  
 **Buscar tabla**  
 Solo en publicaciones de combinación. Haga clic en **Buscar tabla** para buscar una tabla en un árbol de filtros complejo. En una base de datos con relaciones complejas, una tabla se puede combinar con varias tablas y, por tanto, puede aparecer en más de un sitio en el árbol de filtros.  
  
 La tabla real aparece solo en un lugar del árbol y, en otros sitios, la tabla se representa mediante un acceso directo. Un acceso directo a una tabla solo es una referencia a la misma; no muestra los nodos secundarios de la tabla. Un nodo de acceso directo se marca con una flecha de acceso directo y, al expandir ese nodo, se muestra el texto **Haga clic en Buscar tabla para ver la tabla de \<nombre de tabla>** .  
  
 Seleccione un nodo de acceso directo en el panel y haga clic en **Buscar tabla** . El panel se expande y la tabla se resalta. Si hace clic en **Buscar tabla** sin seleccionar un nodo de acceso directo, se abre un cuadro de diálogo **Buscar tabla** .  
  
 **Filter**  
 Contiene la definición de [!INCLUDE[tsql](../../includes/tsql-md.md)] para el filtro seleccionado en el panel de filtros.  

## <a name="publication-access-list"></a>Lista de acceso a la publicación
  La página **Lista de acceso a la publicación** del cuadro de diálogo **Propiedades de la publicación** permite agregar y quitar inicios de sesión, cuentas y grupos de la lista de acceso a la publicación (PAL). La PAL es el mecanismo principal para configurar la seguridad del publicador. Al crear una publicación, la replicación crea una PAL para dicha publicación. La PAL, que ofrece funciones similares a las de una lista de control de acceso de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, contiene una lista de inicios de sesión, cuentas y grupos con permiso de acceso a la publicación.  
  
 Cuando un suscriptor se conecta al publicador o al distribuidor y solicita acceso a la publicación, el inicio de sesión del suscriptor se compara con la información de autenticación de la PAL. Esto proporciona seguridad adicional para el publicador, ya que evita que en el inicio de sesión en el publicador o el distribuidor pueda usarse una herramienta cliente para realizar directamente modificaciones en el publicador. Para obtener más información, vea [Proteger el publicador](../../relational-databases/replication/security/secure-the-publisher.md).  
  
### <a name="options"></a>Opciones  
 **Agregar**  
 Permite agregar una nueva entrada a la lista. Puede agregar solo aquellos nombres de inicio de sesión, cuenta o grupo que ya estén definidos tanto en el publicador como en el distribuidor. Estarán definidos en ambos servidores si se usan cuentas de dominio o si se crean cuentas locales en ambos servidores.  
  
 **Quitar**  
 Permite quitar la entrada seleccionada de la lista.  
  
 **Quitar todo**  
 Quita todas las entradas de la lista.  

## <a name="ftp-snapshot-and-internet"></a>Instantánea de FTP e Internet

-   Establecer propiedades para entregar la instantánea mediante FTP (Protocolo de transferencia de archivos). Para más información, vea [Entregar una instantánea mediante FTP](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md). Si desea usar el FTP para la entrega de instantáneas deberá configurar un servidor FTP. Vea la documentación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows para obtener más información.  
  
    > [!NOTE]  
    >  Si realiza algún cambio en la configuración del FTP deberá generar una nueva instantánea.  
  
-   Establecer propiedades de sincronización web para replicaciones de mezcla en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores, lo que permite sincronizar las suscripciones mediante HTTPS (Protocolo de transferencia de hipertexto seguro). Para poder utilizar la sincronización web deberá configurar un servidor de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS). Para más información, consulte [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
### <a name="options"></a>Opciones  
 **Obtener acceso a archivos de instantánea a través de FTP**  
 Active **Permitir a los suscriptores descargar archivos de instantánea usando FTP (Protocolo de transferencia de archivos)** y especifique el **Nombre del servidor FTP**, el **Número de puerto**, la **Ruta de acceso de la carpeta raíz del servidor FTP**, el **Inicio de sesión**y la **Contraseña**para permitir a los suscriptores usar el FTP para entregar instantáneas.  
  
 Esta opción permite a los suscriptores usar el FTP para recuperar archivos de instantáneas, pero no les obliga a hacerlo. Si se selecciona esta opción, el Asistente para nueva suscripción establece de forma predeterminada que el suscriptor debe recuperar los archivos de instantáneas mediante el FTP. Puede cambiar esta configuración en el cuadro de diálogo **Propiedades de suscripción** . Si permite a los suscriptores tener acceso a los archivos de instantáneas mediante el FTP, debe especificar la carpeta FTP y la ubicación de los archivos de instantáneas en la página **Instantánea** del cuadro de diálogo **Propiedades de la publicación** . Al hacerlo de esta forma, el Agente de instantáneas actualiza automáticamente los archivos en la carpeta FTP cuando se genera una nueva instantánea. Si no establece la carpeta FTP como ubicación, deberá actualizar manualmente los archivos al generar nuevas instantáneas. Para obtener más información, vea [Entregar una instantánea mediante FTP](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md).  
  
 **Sincronización web**  
 Solo replicación de mezcla. Active **Permitir a los suscriptores sincronizarse mediante la conexión a un servidor web**y especifique la dirección de un servidor web para permitir a los suscriptores de mezcla utilizar la sincronización web. El servidor web debe usar SSL (Capa de sockets seguros) y la dirección web debe ser completa (por ejemplo, `https://server.domain.com/synchronize`). Para más información, consulte [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md).  


## <a name="agent-security"></a>Seguridad del agente
  La página **Seguridad del agente** del cuadro de diálogo **Propiedades de la publicación** permite obtener acceso a la configuración de las cuentas en las que se ejecutan los siguientes agentes y realizar conexiones con los equipos de una topología de replicación:  
  
-   Agente de instantáneas para todas las publicaciones.  
  
-   Agente de registro del LOG para todas las publicaciones transaccionales. Existe un Agente de registro del LOG para cada base de datos publicada para la replicación transaccional. Si se cambia la configuración del Agente de registro del LOG, esto afectará a todas las publicaciones transaccionales de una base de datos.  
  
-   Agente de lectura de cola para publicaciones transaccionales que permiten suscripciones de actualización en cola Existe un Agente de lectura de cola para cada base de datos de distribución. Si se cambia la configuración del Agente de lectura de cola, esto afecta a todas las publicaciones transaccionales con suscripciones de actualización en cola que utilizan la misma base de datos de distribución. Para obtener más información sobre la configuración de seguridad del Agente de lectura de cola de replicación, vea [Ver y modificar la configuración de seguridad de la replicación](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 Para obtener más información sobre la configuración de seguridad y los permisos necesarios para cada agente, vea [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
### <a name="options"></a>Opciones  
 **Configuración de seguridad** o **Crear agente**  
 Si se ha creado un trabajo de agente, haga clic en **Configuración de seguridad** para obtener acceso al cuadro de diálogo que permite cambiar la configuración de seguridad de un agente. Si no se ha creado el trabajo de agente, haga clic en **Crear agente** para crear uno y especifique la configuración de seguridad correspondiente.  

## <a name="data-partitions"></a>Particiones de datos
Particiones de datos  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]  
  La página **Particiones de datos** del cuadro de diálogo **Propiedades de la publicación** le permite definir particiones de datos para publicaciones de combinación que utilizan el filtro con parámetros. Después de definir particiones, puede generar instantáneas para estas particiones, proporcionando distintos conjuntos de datos iniciales para diferentes suscriptores sobre la base de las propiedades de conexión (inicio de sesión o nombre del equipo) de los suscriptores. También puede optar por permitir que los suscriptores soliciten la entrega y la generación de instantáneas si no tienen una instantánea disponible para su partición la primera vez que realizan la sincronización. Para más información, consulte [Crear una instantánea para una publicación de mezcla con filtros con parámetros](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
### <a name="options"></a>Opciones  
 **Agregar**  
 Haga clic en **Agregar** para definir una partición. En el cuadro de diálogo **Agregar partición de datos** , especifique valores para **HOST_NAME()** o **SUSER_SNAME()** y defina una programación para actualizar las instantáneas.  
  
 **Editar**  
 Seleccione una partición existente en la cuadrícula y haga clic en **Editar** para editarla.  
  
 **Eliminar**  
 Seleccione una partición existente en la cuadrícula y haga clic en **Eliminar** para eliminarla.  
  
 **Generar instantáneas seleccionadas ahora**  
 Seleccione una o varias particiones en la cuadrícula y haga clic en **Generar instantáneas seleccionadas ahora** para generar instantáneas para estas particiones.  
  
 **Limpiar instantáneas existentes**  
 Seleccione una o varias particiones en la cuadrícula y haga clic en **Limpiar instantáneas existentes** para limpiar las instantáneas de estas particiones.  
  
 **Definir automáticamente una partición y generar una instantánea si es necesario cuando un suscriptor nuevo intente sincronizarse**  
 Seleccione esta opción si desea permitir que los suscriptores soliciten la generación y aplicación de instantáneas. Los suscriptores podrían solicitar esta opción si no tienen una instantánea disponible para su partición la primera vez que realizan la sincronización.  

## <a name="snapshot"></a>Snapshot
Snapshot  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]  
  La página **Instantánea** del cuadro de diálogo **Propiedades de la publicación** permite establecer el formato de instantánea, la ubicación de la carpeta de instantáneas y los scripts que deben ejecutarse antes y después de aplicar la instantánea. La carpeta de instantáneas debe designarse como recurso compartido y debe disponer de los permisos necesarios para que los agentes puedan leer y escribir archivos en ella. Para obtener más información sobre cómo proteger la carpeta adecuadamente, vea [Proteger la carpeta de instantáneas](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
> [!NOTE]  
>  Los cambios requieren una nueva instantánea para la publicación. Para obtener más información, vea [Cambiar las propiedades de la publicación y de los artículos](../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
### <a name="options"></a>Opciones  
 **Formato de instantánea**  
 Permite seleccionar el modo nativo o el modo de carácter para el formato de instantánea.  
  
-   Seleccione **SQL Server nativo: todos los suscriptores deben ser servidores que ejecuten SQL Server** si todos los suscriptores son instancias de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que no son [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)]. El formato nativo de instantánea ofrece el mejor rendimiento.    
-   Seleccione **Carácter: necesario si un publicador o suscriptor no ejecuta SQL Server** si hay suscriptores que ejecutan [!INCLUDE[ssEW](../../includes/ssew-md.md)] o suscriptores que no son de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .    
 **Ubicación de archivos de instantánea**  
 Permite seleccionar la ubicación en la que se almacenarán los archivos de instantánea. Pueden almacenarse en la ubicación predeterminada; también pueden almacenarse en una ubicación alternativa (o en la ubicación predeterminada y en una ubicación alternativa). Los archivos almacenados en una ubicación alternativa pueden comprimirse.  
  
-   Seleccione **Poner los archivos en la carpeta predeterminada** para usar la carpeta de instantáneas predeterminada para el publicador. La ubicación de la carpeta de instantáneas se muestra en este cuadro de diálogo como de solo lectura, ya que los permisos del publicador solamente pueden cambiarse en el cuadro de diálogo **Propiedades del distribuidor** . Para más información, vea [Modificar propiedades de instantáneas](../../relational-databases/replication/snapshot-options.md).    
-   Seleccione **Poner los archivos en la siguiente carpeta** para especificar una ubicación alternativa, o adicional, a la ubicación predeterminada. Escriba una ruta en el cuadro de texto o haga clic en **Examinar** para navegar a una ubicación. Seleccione **Comprimir archivos de instantánea en esta carpeta** para comprimir los archivos en la ubicación de instantáneas alternativa. La ubicación alternativa puede estar en otro servidor, en una unidad de red o en un medio extraíble, como un CD-ROM o un disco extraíble. Para más información, vea [Modificar propiedades de instantáneas](../../relational-databases/replication/snapshot-options.md).  
  
 **Ejecutar scripts adicionales**  
 Permite especificar los scripts que se deben ejecutar antes y después de aplicar la instantánea al suscriptor. Si el **Formato de instantánea** es **Carácter**no se pueden especificar scripts.  
  
 Los scripts son opcionales, pero proporcionan un modo adecuado de ejecutar comandos y aplicar cambios administrativos en los suscriptores. Para obtener más información, vea [Ejecutar scripts antes y después de aplicar la instantánea](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied).  
  
-   Escriba una ruta en el cuadro de texto **Antes de aplicar la instantánea, ejecutar este script** o haga clic en **Examinar** para especificar una ubicación para el script.    
-   Escriba una ruta en el cuadro de texto **Después de aplicar la instantánea, ejecutar este script** o haga clic en **Examinar** para especificar una ubicación para el script. 
  
## <a name="see-also"></a>Consulte también  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Ver y modificar propiedades de publicación](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   

  
  
