---
title: Elementos de informe en el Diseñador de informes (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.components.f1
ms.assetid: 0c34311d-05d6-4bd2-b452-545fa95f8e7f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2c696b87a8c8cf4688e24a0e3177948d339d7443
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66105058"
---
# <a name="report-parts-in-report-designer-ssrs"></a>Elementos de informe en el Diseñador de informes (SSRS)
  En el Diseñador de informes, después de crear tablas, gráficos y otros elementos de informe en un proyecto, puede publicarlos como *elementos de informe* en un servidor de informes o en el sitio de SharePoint integrado con un servidor de informes para que usted y otros usuarios puedan reutilizarlos en otros informes.  
  
 En general, los elementos de informe funcionan de la misma manera en el Diseñador de informes y en el Generador de informes. Para obtener información acerca de la funcionalidad básica, consulte [elementos de informe &#40;generador de informes y SSRS&#41; ](../report-parts-report-builder-and-ssrs.md) en el [documentación del generador de informes](https://go.microsoft.com/fwlink/?LinkId=154494) en msdn.microsoft.com.  
  
 Hay diferencias fundamentales en el modo en que los elementos de informe se usan en el Diseñador de informes. Una diferencia principal es el flujo de trabajo. El Generador de informes habilita la creación colaborativa: Se puede crear un elemento de informe y publicarlo. Puede reutilizarlo, modificarlo y volver a publicarlo. En el Diseñador de informes, la publicación es unidireccional: se puede publicar un elemento de informe en el Diseñador de informes y reutilizarlo. Pero no se puede reutilizar un elemento de informe existente en un informe en el Diseñador de informes. En este tema se elaboran estas diferencias, después de una información general rápida de los elementos de informe.  
  
##  <a name="ComponentWorkflow"></a> Ciclo de vida de la publicación de un elemento de informe  
 ![rs_ComponentCreation](../media/rs-componentcreation.gif "rs_ComponentCreation")  
  
1.  En el Diseñador de informes, la persona A crea un proyecto que contiene un informe con un gráfico que depende de un conjunto de datos incrustado.  
  
2.  La persona A marca el gráfico con su conjunto de datos incrustado para publicarlo. El Diseñador de informes le asigna un identificador único. La persona A implementa el informe en el servidor de informes. El Diseñador de informes publica el gráfico.  
  
3.  La persona B crea un informe en blanco en el Generador de informes y agrega el gráfico a él. El gráfico forma ahora parte del informe de la persona B, junto con el conjunto de datos incrustado. La persona B puede modificar las instancias del gráfico y el conjunto de datos que están en el informe. Esto no tendrá ningún efecto en las instancias del gráfico y el conjunto de datos en el servidor de informes, ni interrumpirá la relación entre las instancias en el informe y en el servidor de informes.  
  
     ![rs_BIDScomponentupdate](../media/rs-bidscomponentupdate.gif "rs_BIDScomponentupdate")  
  
4.  En el Diseñador de informes, la persona A modifica el gráfico en el informe original.  
  
5.  La persona A implementa de nuevo el informe, que vuelve a publicar el gráfico en el servidor, con lo que actualiza el gráfico en el servidor.  
  
6.  En el Generador de informes, la persona B acepta el gráfico actualizado del servidor. De esta forma sobrescribe los cambios que la persona B había realizado en el informe de la persona B.  
  
##  <a name="PublishingComponents"></a> Publicar elementos de informe  
 Al publicar un elemento de informe, el Diseñador de informes le asigna un identificador único. Desde ese momento, mantiene ese identificador, con independencia de lo que cambie. El identificador vincula el elemento de informe original en el informe al elemento de informe. Cuando los autores de otros informes reutilizan el elemento de informe en el Generador de informes, el identificador también vincula el elemento de su informe al elemento de informe.  
  
 Estos son los elementos de informe que puede publicar como elementos de informe:  
  
-   Gráficos  
  
-   Medidores  
  
-   Imágenes e imágenes incrustadas  
  
-   Mapas  
  
-   Parámetros  
  
-   Rectángulos  
  
-   Tablas  
  
-   Matrices  
  
-   Listas  
  
 Si va a publicar un elemento informe que muestra datos, como una tabla, matriz o gráfico, puede basarlo en un conjunto de datos compartido; de lo contrario, al publicar el elemento de informe, el conjunto de datos del que depende se guarda como un conjunto de datos incrustado. Los conjuntos de datos Incrustados pueden estar basados en orígenes del datos incrustados, pero las credenciales no se almacenan en orígenes de datos incrustados. Así, si el elemento de informe depende de un conjunto de datos incrustado que utiliza un origen de datos incrustados, cualquiera que reutilice este elemento de informe tendrá que proporcionar las credenciales para el origen de datos incrustados. Para evitar esto, base los conjuntos de datos incrustados en orígenes de datos compartidos con credenciales almacenadas. Para obtener más información, consulte [elementos de informe y conjuntos de datos en el generador de informes](../report-data/report-parts-and-datasets-in-report-builder.md) en el [documentación del generador de informes](https://go.microsoft.com/fwlink/?LinkId=154494) en msdn.microsoft.com.  
  
 La publicación de un elemento de informe en el Diseñador de informes es un proceso en dos pasos:  
  
1.  Marque los elementos de informe que desea publicar en el cuadro de diálogo **Publicar elementos de informe** .  
  
2.  Implemente el informe.  
  
 Al implementar el informe, el elemento de informe se publica en un sitio de SharePoint o servidor de informes, y otros pueden reutilizarla. Para publicar un elemento de informe, debe disponer de una conexión y de los permisos necesarios en un servidor de informes de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] al implementar el informe.  
  
  
##  <a name="SearchReuseComponents"></a> Reutilizar elementos de informe  
 A diferencia de lo que ocurre en el Generador de informes, no puede buscar y reutilizar un elemento de informe en un proyecto distinto de aquel en el que se creó.  
  
 Los autores del informe que trabajan en el Generador de informes pueden buscar y reutilizar elementos de informe que publique en los informes que crean.  
  
##  <a name="RepublishingComponents"></a> Volver a publicar elementos de informe  
 En el Diseñador de informes, debería actualizar un elemento de informe existente desde dentro del informe en el que se creó. En el Generador de informes, los autores del informe pueden reutilizar el elemento de informe y publicarlo como un nuevo elemento de informe sin reemplazar al elemento de informe que publicó. Si tienen los permisos necesarios, también pueden actualizar el elemento de informe que publicó. Cualquiera con los permisos suficientes para una carpeta en un sitio o servidor puede actualizar los elementos de informe que se almacenan allí. La última actualización sobrescribe las actualizaciones anteriores.  
  
 Puede modificar y, a continuación, volver a publicar el elemento de informe en el sitio o servidor. Los autores de un informe del Generador de informes que hayan agregado ese elemento de informe a un informe son informados del cambio la próxima vez que lo abran. Pueden elegir aceptar sus cambios o no.  
  
 También puede decidir publicar como nuevo un informe que ya haya publicado. En el cuadro de diálogo Publicación de elementos de informe, haga clic en Publicar como un nuevo elemento de informe. Este nuevo elemento de informe tiene un nuevo identificador único y no tiene relación con el elemento de informe anterior.  
  
  
## <a name="see-also"></a>Vea también  
 [Administración de elementos de informe](managing-report-parts.md)  
  
  
