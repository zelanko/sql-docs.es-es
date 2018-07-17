---
title: Generar filtros | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.generatefilters.f1
ms.assetid: be28515c-5d6d-467b-b933-d7c8d97a45b4
caps.latest.revision: 26
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 22be2baf6980f8df813635f3b9d4e4dfd213b818
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37355897"
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
  
     Solo para[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores. La replicación de mezcla le permite especificar el tipo de partición más adecuado para sus datos y aplicación. Si selecciona **Una fila de esta tabla irá a una sola suscripción**, la replicación de mezcla establece la opción de particiones no superpuestas. Las particiones no superpuestas funcionan junto con las particiones precalculadas para aumentar el rendimiento: la finalidad de las particiones no superpuestas es minimizar el costo de carga asociado a las particiones precalculadas. La ventaja en el rendimiento de las particiones no superpuestas es más evidente cuando los filtros con parámetros y de combinación utilizados son más complejos. Si selecciona esta opción, debe asegurarse de que los datos se dividen en particiones de forma que una fila no se pueda replicar en más de un suscriptor. Para obtener más información, vea la sección sobre cómo configurar opciones de partición en el tema [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 Una vez agregado un filtro, haga clic en **Aceptar** para salir y cerrar el cuadro de diálogo. El filtro que ha especificado se analiza y se ejecuta según la tabla de la cláusula SELECT. Si la instrucción de filtro contiene errores de sintaxis u otros problemas, se le notificará y podrá modificar dicha instrucción.  
  
 Una vez analizada la instrucción, la replicación crea los filtros de combinación necesarios. Si todavía no ha configurado el distribuidor del publicador en el que se ejecuta este asistente, se le pedirá que lo configure.  
  
## <a name="see-also"></a>Ver también  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Ver y modificar propiedades de publicación](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Filtrar datos publicados](../../relational-databases/replication/publish/filter-published-data.md)   
 [Join Filters](../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
