---
title: 'Lección 5: automatizar la limpieza y la búsqueda de coincidencias con SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f068d4db-2d56-41b1-bed2-0cffa3ca411d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: ec6f347cdbc6d14e8f621466a1708b8ee9fe7d36
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "65489753"
---
# <a name="lesson-5-automating-the-cleansing-and-matching-using-ssis"></a>Lección 5: Automatización de la limpieza y la búsqueda de coincidencias con SSIS
  En la lección 1, ha creado la base de conocimiento proveedores y la ha usado para limpiar los datos de la lección 2 y buscar los datos coincidentes en la lección 3 mediante el **cliente DQS**de la herramienta. En un escenario real, puede que tenga que extraer datos de un origen que DQS no admita o que desee automatizar el proceso de limpieza y búsqueda de coincidencias sin tener que usar la herramienta **cliente DQS** . SQL Server Integration Services (SSIS) tiene componentes que puede usar para integrar datos de varios orígenes heterogéneos y un componente de **[transformación limpieza de DQS](https://msdn.microsoft.com/library/ee677619.aspx)** para invocar la funcionalidad de limpieza expuesta por DQS. Actualmente, DQS no expone la funcionalidad de búsqueda de coincidencias que debe usar SSIS, pero puede usar la **[transformación agrupación aproximada](../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)** para identificar duplicados en los datos.  
  
 Puede cargar datos en MDS mediante la **característica de almacenamiento provisional basado en entidad**. Cuando crea una entidad en MDS, se crean automáticamente las tablas de ensayo y los procedimientos almacenados correspondientes. Por ejemplo, al crear la entidad supplier, se crearán automáticamente la tabla **STG. supplier_Leaf** y el procedimiento almacenado **STG. udp_Supplier_Leaf** . Use las tablas de ensayo y los procedimientos para crear, actualizar y eliminar miembros de entidad. En esta lección, creará nuevos miembros para la entidad Proveedor. Para cargar datos en el servidor de MDS, el paquete SSIS los carga primero en la tabla de ensayo stg.supplier_Leaf y después desencadena el procedimiento almacenado stg.udp_Supplier_Leaf asociado. Consulte [importación de datos](../master-data-services/overview-importing-data-from-tables-master-data-services.md) para obtener más información.  
  
 En esta lección, realizará las tareas siguientes:  
  
1.  Quitar datos de proveedor en MDS (si ha realizado las cuatro lecciones anteriores). El paquete SSIS que crea en esta lección carga los datos en MDS automáticamente. Antes, cargaba manualmente los datos de proveedor limpios y coincidentes en el servidor de MDS con el Cliente de DQS.  
  
2.  Crear una vista de suscripciones en la entidad Proveedor para exponer los datos de la entidad en otras aplicaciones. Esta acción crea una vista de SQL que comprobará mediante SQL Server Management Studio. No usará esta vista en esta versión del tutorial.  
  
3.  Crear y ejecutar un proyecto de SSIS mediante **SQL Server Data Tools**. El proyecto usa la transformación **limpieza de datos** para enviar una solicitud de limpieza al servidor DQS. DQS no expone todavía la funcionalidad de búsqueda de coincidencias, por lo que usará la transformación **agrupación aproximada** para identificar duplicados.  
  
4.  Comprobar que los datos se crean en MDS mediante Master Data Manager.  
  
5.  Revisar los resultados del proyecto de limpieza de DQS creado por el paquete SSIS y realizar opcionalmente una limpieza interactiva para mejorar la base de conocimiento.  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 1 &#40;requisito previo&#41;: eliminación de los datos de proveedor en MDS](../../2014/tutorials/task-1-prerequisite-removing-supplier-data-in-mds.md)  
  
  
