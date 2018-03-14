---
title: "Propiedades de la publicación, Filtrar filas | Microsoft Docs"
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
f1_keywords:
- sql13.rep.newpubwizard.pubproperties.filterrows.f1
ms.assetid: 2c5fdbed-9b10-4818-98cc-cc6b01351318
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 80da582db33f49ef5fe456eb9351e9b4d6091591
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2018
---
# <a name="publication-properties-filter-rows"></a>Propiedades de la publicación, Filtrar filas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La página **Filtrar filas** del cuadro de diálogo **Propiedades de la publicación** permite realizar operaciones de adición, edición o eliminación:  
  
-   Aplicar filtros de fila estática a artículos de la tabla en publicaciones de instantáneas, transaccionales y de mezcla.  
  
-   Aplicar filtros de fila con parámetros a artículos de la tabla en publicaciones de combinación.  
  
-   Utilizar filtros de combinación para ampliar los filtros de los artículos de tablas de mezcla a artículos de tablas relacionadas.  
  
 Para obtener más información sobre las opciones de filtrado, vea [Filtrar datos publicados](../../relational-databases/replication/publish/filter-published-data.md).  
  
> [!NOTE]  
>  Para agregar, editar o eliminar un filtro, se requiere una nueva instantánea para la publicación y, además, deben reinicializarse todas las suscripciones.  
  
 Para obtener el máximo rendimiento de la aplicación y reducir la cantidad de almacenamiento remoto necesario, o para restringir la disponibilidad de ciertos datos a suscriptores específicos, debe publicar los datos necesarios. La publicación puede incluir tablas sin filtrar y tablas filtradas. Por ejemplo, podría incluir la tabla completa sin filtrar de los productos de la empresa y utilizar filtros de fila para proporcionar una tabla filtrada de clientes para un área específica. Si filtra los datos publicados, podrá:  
  
-   Minimizar la cantidad de datos que se envían a través de la red.  
  
-   Reducir la cantidad de espacio de almacenamiento necesario en el suscriptor.  
  
-   Personalizar las publicaciones y las aplicaciones en función de los requisitos de cada suscriptor.  
  
-   Evitar o reducir los conflictos si los suscriptores actualizan datos, ya que pueden enviarse particiones de datos diferentes a varios suscriptores (dos suscriptores distintos no actualizarán los mismos valores de datos).  
  
-   Evitar la transmisión de datos reservados. Se pueden utilizar filtros de fila y filtros de columna para restringir el acceso de un suscriptor a los datos. Para la replicación de mezcla, existen consideraciones de seguridad que se deben tener en cuenta si utiliza un filtro con parámetros que incluya HOST_NAME(). Para obtener más información, vea la sección sobre cómo filtrar con HOST_NAME() en el tema [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
## <a name="options"></a>.  
 **Tablas filtradas**  
 Este panel se llena con filtros según se agregan a los artículos de la tabla en la publicación. Las tablas con filtros de fila se muestran como nodos de nivel superior en el panel. En las publicaciones de combinación, las tablas cuyo filtro se ha ampliado a filtro de combinación se muestran como nodos secundarios.  
  
 **Agregar**  
 Haga clic en **Agregar** para abrir un cuadro de diálogo que permite filtrar artículos de la tabla. Si hace clic en **Agregar** en una publicación de instantáneas o transaccional, se abre inmediatamente un cuadro de diálogo. Si hace clic en **Agregar** en una publicación de combinación, se muestran tres opciones: **Agregar filtro**, **Agregar combinación para ampliar el filtro seleccionado**y **Generar filtros automáticamente**.  
  
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
  
 La tabla real aparece solo en un lugar del árbol y, en otros sitios, la tabla se representa mediante un acceso directo. Un acceso directo a una tabla solo es una referencia a la misma; no muestra los nodos secundarios de la tabla. Un nodo de acceso directo se marca con una flecha de acceso directo y, al expandir ese nodo, se muestra el texto **Haga clic en Buscar tabla para ver la tabla de \<nombre de tabla>**.  
  
 Seleccione un nodo de acceso directo en el panel y haga clic en **Buscar tabla** . El panel se expande y la tabla se resalta. Si hace clic en **Buscar tabla** sin seleccionar un nodo de acceso directo, se abre un cuadro de diálogo **Buscar tabla** .  
  
 **Filter**  
 Contiene la definición de [!INCLUDE[tsql](../../includes/tsql-md.md)] para el filtro seleccionado en el panel de filtros.  
  
## <a name="see-also"></a>Ver también  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Crear y aplicar la instantánea inicial](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [Reinicializar una suscripción](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [Ver y modificar propiedades de publicación](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Filtrar datos publicados](../../relational-databases/replication/publish/filter-published-data.md)   
 [Join Filters](../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
