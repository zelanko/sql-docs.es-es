---
title: Generar filtros | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.generatefilters.f1
ms.assetid: be28515c-5d6d-467b-b933-d7c8d97a45b4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 14ccac181a4b76f8fc0423d6e00b20f91f8ea9cc
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/05/2019
ms.locfileid: "67581360"
---
# <a name="generate-filters"></a>Generar filtros
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El cuadro de diálogo **Generar filtros** le permite definir un filtro de filas en una tabla de una publicación de combinación; la replicación extenderá automáticamente el filtro a otras tablas relacionadas con relaciones de clave externa. Por ejemplo, si define un filtro en una tabla de clientes para que solo contenga datos de clientes franceses, la replicación extiende el filtro de forma que los pedidos y las tablas de detalles de pedidos relacionados solo contengan información relativa a los clientes franceses.  
  
## <a name="options"></a>Opciones  
 El cuadro de diálogo presenta un proceso de tres pasos para crear un filtro de fila en una tabla. A continuación, el filtro se extiende a las tablas relacionadas con la tabla filtrada mediante relaciones de clave principal y de clave externa. Por ejemplo, dadas las tablas **Customer**, **SalesOrderHeader**y **SalesOrderDetail**, con una relación entre **Customer** y **SalesOrderHeader**y una relación entre **SalesOrderHeader** y **SalesOrderDetail**, al aplicar un filtro de filas a **Customer**, la replicación extenderá dicho filtro a **SalesOrderHeader** y **SalesOrderDetail**.  
  
1.  **Seleccione la tabla que desea filtrar.**  
  
     Seleccione una tabla del cuadro de lista desplegable. Las tablas solo se mostrarán en el cuadro de lista si se han seleccionado en la página **Artículos** .  
  
2.  **Complete la instrucción de filtro para identificar las filas de la tabla que recibirán los suscriptores.**  
  
     Defina una nueva instrucción de filtro. El cuadro de lista **Columnas** muestra todas las columnas que va a publicar en la tabla seleccionada en **Seleccione la tabla que desea filtrar**. El área de texto **Instrucción de filtro** incluye el texto predeterminado, que tiene este formato:  
  
     `SELECT <published_columns> FROM [tableowner].[tablename] WHERE`  
  
     No se puede cambiar este texto; escriba la cláusula de filtro después de la palabra clave WHERE utilizando sintaxis estándar [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
    > [!IMPORTANT]  
    >  Por motivos de rendimiento, se recomienda que no aplique funciones a nombres de columnas en las cláusulas de los filtros de fila con parámetros, como `LEFT([MyColumn]) = SUSER_SNAME()`. Si utiliza HOST_NAME en una cláusula de filtro y reemplaza el valor HOST_NAME, puede que sea necesario convertir los tipos de datos utilizando CONVERT. Para obtener más información acerca de las prácticas recomendadas para este caso, vea la sección "Reemplazar el valor de HOST_NAME()" del tema [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
3.  **Especifique cuántas suscripciones recibirán datos de esta tabla.**  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

     [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] and later versions only. Merge replication allows you to specify the type of partitions that are best suited to your data and application. If you select **A row from this table will go to only one subscription**, merge replication sets the nonoverlapping partitions option. Nonoverlapping partitions work in conjunction with precomputed partitions to improve performance, with nonoverlapping partitions minimizing the upload cost associated with precomputed partitions. The performance benefit of nonoverlapping partitions is more noticeable when the parameterized filters and join filters used are more complex. If you select this option, you must ensure that the data is partitioned in such a way that a row cannot be replicated to more than one Subscriber. For more information, see the section "Setting 'partition options'" in the topic [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 Una vez agregado un filtro, haga clic en **Aceptar** para salir y cerrar el cuadro de diálogo. El filtro que ha especificado se analiza y se ejecuta según la tabla de la cláusula SELECT. Si la instrucción de filtro contiene errores de sintaxis u otros problemas, se le notificará y podrá modificar dicha instrucción.  
  
 Una vez analizada la instrucción, la replicación crea los filtros de combinación necesarios. Si todavía no ha configurado el distribuidor del publicador en el que se ejecuta este asistente, se le pedirá que lo configure.  
  
## <a name="see-also"></a>Consulte también  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Ver y modificar propiedades de publicación](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Filtrar datos publicados](../../relational-databases/replication/publish/filter-published-data.md)   
 [Join Filters](../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
