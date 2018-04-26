---
title: Agregar o editar filtro | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.rep.newpubwizard.addeditfilter.f1
ms.assetid: bdd7c71d-1c59-4044-bfe8-c85f908345bb
caps.latest.revision: 27
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 332d02a43291257c567b93a4d689e932d67e7a8f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="add-or-edit-filter"></a>Agregar filtro o Editar filtro
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Los cuadros de diálogo **Agregar filtro** y **Editar filtro** le permiten agregar y editar filtros de filas estáticos y filtros de filas con parámetros.  
  
> [!NOTE]  
>  La edición de un filtro en una publicación existente requiere una nueva instantánea para la publicación. Si una publicación tiene suscripciones, es necesario reinicializar las suscripciones. Para obtener más información sobre los cambios de propiedad, consulte [Cambiar las propiedades de la publicación y de los artículos](../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
 Todos los tipos de publicaciones pueden incluir filtros estáticos; las publicaciones de combinación también pueden incluir filtros con parámetros. Se evalúa un filtro estático cuando se crea la publicación: todos los Suscriptores a la publicación reciben los mismos datos. Un filtro parametrizado se evalúa durante la sincronización de la replicación: Suscriptores diferentes pueden recibir particiones distintas de datos según el inicio de sesión o nombre de equipo de cada Suscriptor. Haga clic en el vínculo **Instrucciones de ejemplo** del cuadro de diálogo para ver ejemplos de cada tipo de filtro. Para obtener más información sobre las opciones de filtrado, consulte [Filtrar datos publicados](../../relational-databases/replication/publish/filter-published-data.md).  
  
 Mediante los filtros de fila, puede especificar un subconjunto de filas de la tabla que desea publicar. Puede utilizar filtros de filas para eliminar filas que no necesitan ver los usuarios (como las filas que contienen información importante o confidencial) o crear distintas particiones de datos que se enviarán a distintos suscriptores. La publicación de distintas particiones de datos para distintos suscriptores también puede ayudar a evitar conflictos que podrían causar la actualización simultánea de los mismos datos realizada por varios suscriptores.  
  
## <a name="options"></a>Opciones  
 Este cuadro de diálogo incluye un proceso de dos pasos para las publicaciones transaccionales y de instantáneas y un proceso de tres pasos para las publicaciones de combinación. Todos los tipos de publicaciones requieren que seleccione la tabla que desea filtrar y una o más columnas que se incluirán en el filtro, en donde el filtro se define como una cláusula WHERE estándar.  
  
1.  **Seleccione la tabla que desea filtrar**  
  
     Si va a editar un filtro existente, no se puede cambiar la selección de la tabla. Si va a agregar un nuevo filtro, seleccione una tabla del cuadro de lista desplegable. Las tablas solo se mostrarán en el cuadro de lista si se han seleccionado en la página **Artículos** y no presentan un filtro de fila. Si la tabla presenta un filtro de fila y desea definir uno nuevo:  
  
    1.  Haga clic en **Cancelar** en el cuadro de diálogo **Agregar filtro** .  
  
    2.  Seleccione la tabla en el panel de filtros de la página **Filtrar filas de tabla** y haga clic en **Editar**.  
  
    3.  Edite un filtro existente en el cuadro de diálogo **Editar filtro** .  
  
2.  **Complete la instrucción de filtro para identificar las filas de la tabla que recibirán los suscriptores**  
  
     Defina una nueva instrucción de filtro o edite una existente. El cuadro de lista **Columnas** muestra todas las columnas que va a publicar en la tabla seleccionada en **Seleccione la tabla que desea filtrar**. El área de texto **Instrucción de filtro** incluye el texto predeterminado, que tiene este formato:  
  
     `SELECT <published_columns> FROM [schema].[tablename] WHERE`  
  
     No se puede cambiar este texto; escriba la cláusula de filtro después de la palabra clave WHERE utilizando sintaxis estándar [!INCLUDE[tsql](../../includes/tsql-md.md)] . Si el publicador es un publicador de Oracle, la cláusula WHERE debe seguir la sintaxis de consultas de Oracle. Evite utilizar filtros complejos en la medida de lo posible. Tanto los filtros estáticos como los que utilizan parámetros aumentan el tiempo de procesamiento de las publicaciones, por lo que deberá escribir las instrucciones de filtro de la forma más sencilla posible.  
  
    > [!IMPORTANT]  
    >  Por motivos de rendimiento, se recomienda no aplicar funciones a los nombres de columna en las cláusulas de los filtros de fila con parámetros, como `LEFT([MyColumn]) = SUSER_SNAME()`. Si utiliza HOST_NAME en una cláusula de filtro y reemplaza el valor HOST_NAME, puede que sea necesario convertir los tipos de datos utilizando CONVERT. Para obtener más información acerca de las prácticas recomendadas para este caso, vea la sección "Reemplazar el valor de HOST_NAME()" del tema [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
3.  **Especifique cuántas suscripciones recibirán datos de esta tabla**  
  
     [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores únicamente; solo para la replicación de mezcla. La replicación de mezcla le permite especificar el tipo de partición más adecuado para sus datos y aplicación. Si selecciona **Una fila de esta tabla irá a una sola suscripción**, la replicación de mezcla establece la opción de particiones no superpuestas. Las particiones no superpuestas funcionan junto con las particiones precalculadas para aumentar el rendimiento: la finalidad de las particiones no superpuestas es minimizar el costo de carga asociado a las particiones precalculadas. La ventaja en el rendimiento de las particiones no superpuestas es más evidente cuando los filtros con parámetros y de combinación utilizados son más complejos. Si selecciona esta opción, debe asegurarse de que los datos se dividen en particiones de forma que una fila no se pueda replicar en más de un suscriptor. Para obtener más información, vea la sección sobre cómo configurar opciones de partición en el tema [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 Una vez agregado o editado un filtro, haga clic en **Aceptar** para guardar los cambios y cerrar el cuadro de diálogo. El filtro que ha especificado se analiza y se ejecuta según la tabla de la cláusula SELECT. Si la instrucción de filtro contiene errores de sintaxis u otros problemas, se le notificará para que pueda editar la instrucción de filtro.  
  
## <a name="see-also"></a>Ver también  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Ver y modificar propiedades de publicación](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Filtrar datos publicados](../../relational-databases/replication/publish/filter-published-data.md)   
 [Join Filters](../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
