---
title: Elementos de informe y conjuntos de datos en el Generador de informes | Microsoft Docs
ms.custom: 
ms.date: 09/16/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-data
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1fe86481-9c41-4535-a4b7-c7c4d780cab6
caps.latest.revision: "9"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8333a60403a32321c8796bb2041d6e95e39160ce
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2018
---
# <a name="report-parts-and-datasets-in-report-builder"></a>Elementos de informe y conjuntos de datos en el Generador de informes
  En el Generador de informes, la manera más fácil de incluir datos en un informe es agregar elementos de informe de la galería de elementos de informe. Los elementos de informe contienen los conjuntos de datos de los que dependen, que se conocen como *conjuntos de datos dependientes*. Los conjuntos de datos dependientes están ubicados en orígenes de datos compartidos y pueden ser conjuntos de datos incrustados o conjuntos de datos compartidos. Para más información, vea [Elementos de informe](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md).  
  
 Otra manera fácil de incluir datos en un informe es usar un conjunto de datos compartido. Para más información, vea [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Adding"></a> Agregar al informe un elemento de informe con conjuntos de datos dependientes  
 Al agregar un elemento de informe a un informe, también se agregan los conjuntos de datos dependientes que contiene. Dado que un elemento de informe podría incluir un rectángulo con muchos otros elementos de informe, puede agregar varios conjuntos de datos dependientes al informe. Cada conjunto de datos compartido es una referencia independiente; el origen de datos compartido del que depende no se agrega al informe. Cada conjunto de datos incrustado también agrega el origen de datos incrustado o compartido del que depende.  
  
 Las credenciales para un origen de datos incrustados no se guardan como parte del elemento de informe. Si se agrega al informe un origen del datos incrustado, se le pedirán las credenciales al ejecutar el informe. Para evitar que se le pidan las credenciales, use elementos de informe que están ubicados en orígenes de datos compartidos con las credenciales almacenadas.  
  
 Después de agregar al informe un elemento de informe, no hay ninguna diferencia entre los conjuntos de datos agregados y los conjuntos de datos incrustados o compartidos que cree. Puede ver los conjuntos de datos adicionales en el panel Datos de informe. Los conjuntos de datos incrustados aparecen bajo el origen de datos compartido correspondiente y los conjuntos de datos compartidos aparecen bajo la carpeta de conjuntos de datos compartidos.  
  
##  <a name="Customizing"></a> Personalizar conjuntos de datos dependientes  
 Después de agregar elementos de informe al informe, podría obtener una vista previa y decidir realizar cambios en los datos. Qué cambios puede realizar depende del tipo de conjunto de datos con el que esté trabajando.  
  
 Para cambiar los datos y las opciones de datos de un conjunto de datos incrustado, puede modificar las propiedades de conjunto de datos, incluso la consulta, como si hubiera creado el conjunto de datos usted mismo.  
  
 Para cambiar los datos y las opciones de datos de un conjunto de datos compartido, solo puede cambiar la definición del conjunto de datos compartido en el servidor de informes si tiene los permisos necesarios. También puede personalizar la instancia del conjunto de datos compartido en el informe agregando filtros, agregando campos calculados y cambiando opciones de datos como la distinción entre mayúsculas y minúsculas. Para más información, vea [Conjuntos de datos incrustados y compartidos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md).  
  
 Para más información sobre cómo cambiar la definición de un conjunto de datos compartido o cómo mostrar los cambios de datos más recientes de un conjunto de datos compartidos en el informe, vea [Crear un conjunto de datos compartido o un conjunto de datos incrustado &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md) y [Agregar, editar y actualizar campos en el panel Datos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md).  
  
##  <a name="Publishing"></a> Publicar conjuntos de datos dependientes como conjuntos de datos compartidos  
 Al publicar un elemento de informe que tiene conjuntos de datos dependientes, tiene la opción de publicar cada conjunto de datos como un conjunto de datos compartido o como un conjunto de datos incrustado que sigue estando incrustado en el elemento de informe.  
  
 Si selecciona la opción de conjunto de datos compartido, el conjunto de datos se guarda en el servidor de informes como una definición de conjunto de datos compartido. En el informe, cada elemento de informe que use ese conjunto de datos se actualiza para señalar al conjunto de datos compartido que se encuentra ahora en el servidor de informes. Como consecuencia, suceden dos cosas:  
  
1.  En el cuadro de diálogo de publicación, cada conjunto de datos compartido que se ha publicado se quita de la lista de elementos disponibles para la publicación.  
  
2.  Al salir del Generador de informes o iniciar otro informe, se le pide que guarde el informe. Si no lo guarda, la próxima vez que abra este informe y publique elementos informe, podría publicar nuevas copias de los mismos conjuntos de datos. Para evitar que se guarden varias copias de conjuntos de datos compartidos en el servidor de informes, se recomienda que guarde el informe.  
  
> [!IMPORTANT]  
>  Para asegurarse de que usted y otros usuarios pueden seguir usando correctamente los datos de un conjunto de datos compartido, debe entender los principios básicos sobre la protección de los elementos de informe. Para más información, vea [Proteger los elementos de un conjunto de datos compartido](../../reporting-services/security/secure-shared-dataset-items.md).  
  
## <a name="see-also"></a>Ver también  
 [Vista de diseño de informe &#40;Generador de informes&#41;](../../reporting-services/report-builder/report-design-view-report-builder.md)   
 [Seguridad &#40;Generador de informes&#41;](../../reporting-services/report-builder/security-report-builder.md)   
 [Elementos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)   
 [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
