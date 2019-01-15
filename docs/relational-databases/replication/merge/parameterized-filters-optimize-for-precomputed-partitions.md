---
title: Optimización del rendimiento de los filtros con parámetros con particiones calculadas previamente | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- precomputed partitions [SQL Server replication]
- merge replication precomputed partitions [SQL Server replication]
- merge replication precomputed partitions [SQL Server replication], about precomputed partitions
ms.assetid: 85654bf4-e25f-4f04-8e34-bbbd738d60fa
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a7a882660203ee2c23e1cdb6cb9dbf6aa7df407d
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54124305"
---
# <a name="parameterized-filters---optimize-for-precomputed-partitions"></a>Filtros con parámetros: optimizar para las particiones precalculadas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Las particiones precalculadas son una optimización del rendimiento que se puede utilizar con publicaciones de combinación filtradas. Las particiones precalculadas son también un requisito para utilizar registros locales en publicaciones filtradas. Para obtener más información sobre los registros lógicos, vea [Agrupar cambios en filas relacionadas con registros lógicos](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
 Cuando un suscriptor se sincroniza con un publicador, el publicador debe evaluar los filtros del suscriptor para determinar qué filas pertenecen a la partición, o conjunto de datos, de ese suscriptor. Este proceso de determinar la pertenencia a particiones de los cambios en el publicador para cada suscriptor que recibe un conjunto de datos filtrados se denomina *evaluación de particiones*. Sin las particiones precalculadas, la evaluación de particiones debe realizarse para cada cambio efectuado en una columna filtrada del publicador desde la última vez que se ejecutó el Agente de mezcla para un suscriptor concreto, y este proceso tiene que repetirse para cada suscriptor que se sincroniza con el publicador.  
  
 No obstante, si el publicador y el suscriptor se están ejecutando en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o una versión posterior y utiliza particiones precalculadas, la pertenencia a particiones de todos los cambios efectuados en el publicador se calcula previamente y se mantiene en el momento en que se realizan los cambios. Como resultado, cuando un suscriptor se sincroniza con el publicador, puede empezar a descargar inmediatamente los cambios relativos a su partición sin tener que pasar por el proceso de evaluación de particiones. Esto puede producir importantes mejoras de rendimiento cuando una publicación tiene un número elevado de cambios, suscriptores o artículos.  
  
 Además de utilizar particiones precalculadas, genere instantáneas previamente o permita a los suscriptores que soliciten la generación y aplicación de instantáneas la primera vez que se sincronizan. Utilice una de estas opciones o las dos para proporcionar instantáneas para publicaciones que utilicen filtros con parámetros. Si no especifica una de estas opciones, las suscripciones se inicializan utilizando una serie de instrucciones SELECT e INSERT, en lugar de la utilidad **bcp** ; este proceso es mucho más lento. Para más información, consulte [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
 **Para utilizar particiones precalculadas**  
  
 Las particiones precalculadas están habilitadas de forma predeterminada en todas las publicaciones nuevas y existentes que se ajustan a las directrices indicadas anteriormente. La configuración se puede cambiar a través de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o mediante programación. Para más información, consulte [Optimize Parameterized Row Filters](../../../relational-databases/replication/publish/optimize-parameterized-row-filters.md).  
  
## <a name="requirements-for-using-precomputed-partitions"></a>Requisitos para utilizar particiones precalculadas  
 Si se reúnen los siguientes requisitos, las publicaciones de combinación nuevas se crean, de forma predeterminada, con las particiones precalculadas habilitadas, y las publicaciones existentes se actualizan de forma automática para utilizar esta característica. Si una publicación no reúne los requisitos se puede cambiar y, a continuación, habilitar las particiones precalculadas. Si algunos artículos satisfacen estos requisitos y otros no, considere la posibilidad de crear dos publicaciones, una de ellas habilitada para particiones precalculadas.  
  
### <a name="requirements-for-filter-clauses"></a>Requisitos para cláusulas de filtro  
  
-   Cualquier función utilizada en los filtros de fila con parámetros, como HOST_NAME() y SUSER_SNAME(), debe aparecer directamente en la cláusula de filtro con parámetros en lugar de anidarse dentro de una vista o función dinámica. Para obtener más información sobre estas funciones, consulte [HOST_NAME &#40;Transact-SQL&#41;](../../../t-sql/functions/host-name-transact-sql.md), [SUSER_SNAME &#40;Transact-SQL&#41;](../../../t-sql/functions/suser-sname-transact-sql.md) y [Filtros de fila con parámetros](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
-   Los valores devueltos para cada suscriptor no deben cambiarse una vez creada la partición. Por ejemplo, si utiliza HOST_NAME() en un filtro, y no reemplaza el valor de HOST_NAME(), no cambie el nombre del equipo en el suscriptor.  
  
-   Los filtros de combinación no deben contener funciones dinámicas (funciones como HOST_NAME() y SUSER_SNAME() que evalúan a un valor diferente dependiendo del suscriptor que se está sincronizando). Solo los filtros de fila con parámetros deben contener funciones dinámicas.  
  
-   No se pueden usar funciones no deterministas en una cláusula de filtro. Para obtener más información acerca de las funciones no deterministas, vea [Deterministic and Nondeterministic Functions](../../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
-   Las vistas a las que se hace referencia en las cláusulas de filtro de combinación o cláusulas de filtro con parámetros no deben contener funciones dinámicas.  
  
-   No deben existir relaciones de filtro de combinación circulares en la publicación.  
  
### <a name="database-collation"></a>Intercalación de base de datos  
  
-   Cuando se utilizan las particiones precalculadas, siempre se utiliza la intercalación de la base de datos al realizar comparaciones, en lugar de la intercalación de la tabla o columna. Considere el caso siguiente:  
  
    -   Una base de datos con una intercalación que distingue entre mayúsculas y minúsculas contiene una tabla con una intercalación que no distingue entre mayúsculas y minúsculas.  
  
    -   La tabla contiene una columna **ComputerName**que se compara con el nombre de host del suscriptor en un filtro con parámetros.  
  
    -   La tabla contiene una fila con el valor "MYCOMPUTER" y otra fila con el valor "mycomputer" en esta columna.  
  
     Si el suscriptor se sincroniza con un nombre de host de "mycomputer", el suscriptor recibe solamente una fila porque la comparación distingue entre mayúsculas y minúsculas (la intercalación de la base de datos). Si no se utilizan particiones precalculadas, el suscriptor recibe ambas filas porque la tabla tiene una intercalación que no distingue entre mayúsculas y minúsculas.  
  
## <a name="performance-of-precomputed-partitions"></a>Rendimiento de las particiones precalculadas  
 Existe un pequeño costo de rendimiento con las particiones precalculadas cuando se cargan cambios desde el suscriptor al publicador, pero la mayor parte del tiempo de procesamiento de mezcla se dedica a evaluar las particiones y descargar los cambios del publicador al suscriptor, por lo que la ganancia neta puede ser importante. La ventaja en cuanto al rendimiento variará dependiendo del número de suscriptores que se sincronicen de forma simultánea y del número de actualizaciones por sincronización que desplacen filas de una partición a otra.  
  
## <a name="see-also"></a>Consulte también  
 [Filtros de fila con parámetros](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  
