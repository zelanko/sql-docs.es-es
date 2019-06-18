---
title: Elementos de informe (Generador de informes y SSRS) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10543"
ms.assetid: 957f664c-8a7a-4532-b5a6-5f859c5840bd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3fbef30f8a5bf5658376a37144c8f770317d6981
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65576726"
---
# <a name="report-parts-report-builder-and-ssrs"></a>Elementos de informe (Generador de informes y SSRS)
  Las tablas, las matrices, los gráficos y las imágenes que se incluyen en los informes, se pueden publicar como *elementos de informe*. Se trata de elementos de informe paginado que se han publicado por separado en un servidor de informes y se pueden volver a usar en otros informes paginados. Los elementos de informe tienen una extensión de archivo .rsc.  
  
 Con los elementos de informe, los grupos de trabajo pueden aprovechar ahora los diversos puntos fuertes y roles de los miembros del equipo. Por ejemplo, si es el encargado de crear los gráficos, puede guardarlos como partes independientes que usted y sus colaboradores pueden reutilizar en otros informes. Puede publicar los elementos de informe en un servidor de informes o sitio de SharePoint integrado con un servidor de informes. Puede reutilizarlas en varios informes y puede actualizarlas en el servidor.  
  
 El elemento de informe que agrega a un informe mantiene una relación con la instancia del elemento de informe en el sitio o servidor por medio de un identificador único. Después de agregar elementos de informe de un sitio o servidor a un informe, puede modificarlas, de forma independiente del elemento de informe original en el sitio o servidor. Puede aceptar las actualizaciones realizadas por otros usuario al elemento de informe en el sitio o servidor, y puede volver a guardar el elemento de informe modificado en el sitio o servidor, agregando un nuevo elemento de informe o sobrescribiendo el original, si tiene los permisos necesarios.  
  
##  <a name="ComponentWorkflow"></a> El ciclo de vida de un elemento de informe  
 ![rs_ComponentCreation](../../reporting-services/report-design/media/rs-componentcreation.gif "rs_ComponentCreation")  
  
1.  La persona A crea un informe con un gráfico que depende de un conjunto de datos incrustado.  
  
2.  La persona A decide publicar el gráfico en el servidor de informes. El Generador de informes asigna un identificador único al gráfico publicado. La persona A decide no compartir el conjunto de datos, de modo que el conjunto de datos permanece incrustado en el gráfico.  
  
3.  La persona B crea un informe en blanco, busca en la galería de elementos de informe, encuentra el gráfico y lo agrega a su informe. El gráfico forma ahora parte del informe de la persona B, junto con el conjunto de datos incrustado. La persona B puede modificar las instancias del gráfico y el conjunto de datos que están en el informe. Esto no tendrá ningún efecto en las instancias del gráfico y el conjunto de datos en el servidor de informes, ni interrumpirá la relación entre las instancias en el informe y en el servidor de informes.  
  
     ![rs_componentupdate](../../reporting-services/report-design/media/rs-componentupdate.gif "rs_componentupdate")  
  
4.  La persona C agrega el gráfico a un informe y lo cambia de gráfico de barras a gráfico circular.  
  
5.  La persona C tiene los permisos necesarios para sobrescribir el gráfico en el servidor; lo hace así y vuelve a publicarlo en el servidor. Así se actualiza la copia publicada del gráfico en el servidor. La persona C decide también no compartir el conjunto de datos, de modo que el conjunto de datos permanece incrustado en el gráfico.  
  
6.  La persona B acepta el gráfico actualizado del servidor. De esta forma sobrescribe los cambios que la persona B había realizado en el informe de la persona B.  
  
  
##  <a name="PublishingComponents"></a> Publicar elementos de informe  
 Al publicar un elemento de informe, el Generador de informes le asigna un identificador único, distinto del nombre del elemento de informe. El Generador de informes conserva ese identificador, independientemente de qué se cambie del elemento de informe. El identificador vincula el elemento de informe original en el informe al elemento de informe. Cuando los autores de otros informes reutilizan el elemento de informe, el identificador también vincula el elemento de su informe al elemento de informe en el servidor de informes.  
  
 Estos son los elementos de informe que puede publicar como elementos de informe:  
  
-   Gráficos  
  
-   Medidores  
  
-   Imágenes  
  
-   Mapas  
  
-   Parámetros  
  
-   Rectángulos  
  
-   Tablas  
  
-   Matrices  
  
-   Listas  
  
 Al publicar un elemento de informe que muestra datos, por ejemplo una tabla, matriz o gráfico, el conjunto de datos del que depende el elemento de informe se guarda con él, como un conjunto de datos incrustado en el elemento. También puede guardar el conjunto de datos por separado, como conjunto de datos compartido que usted y otros pueden utilizar como punto de partida para otros elementos de informe. Para obtener más información, vea [Elementos de informe y conjuntos de datos en el Generador de informes](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md).  
  
 Algunos elementos de informe pueden contener otros elementos de informe. Por ejemplo, una tabla puede contener un gráfico y un rectángulo puede contener una matriz y un gráfico. Al publicar un elemento de informe que contiene otros elementos de informe, se guardan como una unidad. Los demás elementos de informe se guardan incrustados en el elemento de informe que los contiene. No puede actualizarlos por separado, ni guardar los elementos del contenedor como elementos de informe independientes.  
  
 Para obtener más información sobre cómo publicar elementos de informe, vea [Publicar y volver a publicar elementos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/publish-and-republish-report-parts-report-builder-and-ssrs.md).  
  
### <a name="modifying-report-part-metadata"></a>Modificar los metadatos del elemento de informe  
 Puede publicar elementos de informe con la configuración predeterminada en una ubicación predeterminada, o guardar cada elemento de informe en una ubicación distinta y modificar los metadatos, por ejemplo el título y la descripción.  
  
 Es aconsejable dar un nombre claro y una descripción al elemento de informe al publicarlo, porque esto ayuda a los usuarios a identificarlo cuando la buscan. De lo contrario, podría llegar a tener muchos elementos de informe con nombres parecidos en el sitio o el servidor. Considere la posibilidad de usar convenciones de nomenclatura para mostrar las relaciones entre los elementos de informe y sus elementos dependientes.  
  
 También es aconsejable guardar los orígenes de datos compartidos, los conjuntos de datos compartidos y los elementos de informe que dependen de ellos en la misma carpeta.  
  
 La descripción se puede editar en el panel Propiedades.  
  
  
##  <a name="ReusingComponents"></a> Reutilizar elementos de informe  
 La manera más fácil de crear un informe es agregar un elemento de informe existente, como una tabla o un gráfico, de la galería de elementos de informe a su informe. Después de agregarla a un informe, puede modificarla como convenga o aceptar las actualizaciones del servidor. Los cambios realizados en el elemento del informe no afectan a la instancia del elemento de informe publicada en el sitio o servidor, ni a la relación entre las instancias del informe y del sitio o servidor. Si tiene los permisos necesarios, puede volver a guardar la copia actualizada en el sitio o servidor. Si otro usuario modifica la copia del sitio o servidor, puede decidir mantener su copia como está o actualizarla para que sea como la copia del sitio o servidor.  
  
### <a name="searching-for-report-parts"></a>Buscar elementos de informe  
 Pueden buscar elementos de informe en la galería de elementos de informe para agregarlos a un informe. Puede filtrar los elementos de informe por el nombre completo o solo parte de él, quién lo ha creado, quién lo ha modificado por última vez, cuándo se modificaron por última vez, dónde están almacenados, o bien el tipo de elemento de informe. Por ejemplo, podría buscar todos los gráficos creados la semana pasada por uno de sus colaboradores.  
  
 Puede ver los resultados de la búsqueda como miniaturas o como lista, y ordenar los resultados de la búsqueda por nombre, fechas de creación y modificación, y autor. Para obtener más información, vea [Buscar elementos de informe y establecer una carpeta predeterminada &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs.md).  
  
### <a name="what-comes-with-a-report-part"></a>Componentes de un elemento de informe  
 Al agregar un elemento de informe al informe, también agrega todo lo que debe tener para que funcione. Por ejemplo, cualquier objeto que muestre datos depende de un conjunto de datos, es decir, una consulta y una conexión a un origen de datos. También puede tener uno o varios parámetros. Todos los elementos de los que depende son sus *dependencias*y todos ellos, o punteros que los señalan, se incluyen con el elemento de informe al agregarlo a un informe. El conjunto de datos y los parámetros se enumeran en el panel Datos de informe en el informe.  
  
 El conjunto de datos para el elemento de informe se puede incrustar en el elemento de informe, o puede ser un conjunto de datos independiente y compartido al que el elemento de informe señala. Si se incrusta en el elemento de informe, quizá puede modificarlo. Si es un conjunto de datos compartido, es un objeto independiente para el que necesitaría permisos. Para más información sobre los conjuntos de datos insertados y compartidos, vea [Conjuntos de datos de informe &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md).  
  
### <a name="resolving-naming-conflicts"></a>Solucionar conflictos de nomenclatura  
 Cuando agrega un elemento de informe, el Generador de informes corrige los conflictos de nombre. Por ejemplo, si ya tiene Chart1 en un informe y agrega un elemento de informe denominado Chart1, el Generador de informes cambia el nombre del nuevo elemento de informe a Chart2 automáticamente. Si ya tiene Dataset1 en un informe y agrega un elemento de informe que hace referencia a otro conjunto de datos que también se llama Dataset1, el Generador de informes cambia el nombre del nuevo a Dataset2 y actualiza las referencias.  
  
### <a name="adding-more-than-one-report-part"></a>Agregar más de un elemento de informe  
 Es posible agregar un número ilimitado de elementos de informe en los informes. Sin embargo, un elemento de informe solo se puede agregar de uno en uno. Puede agregar incluso varias instancias de un elemento de informe al mismo informe. Todas tendrán nombres únicos, pero serán instancias del mismo elemento de informe en el servidor y tendrán el mismo identificador único.  
  
 Si agrega otro elemento de informe que usa un conjunto de datos idéntico a otro que ya está en el informe, el asistente no agrega otra versión de ese conjunto de datos al informe; redirige las referencias del elemento de informe hacia el conjunto de datos existente. Para obtener más información, vea [Elementos de informe y conjuntos de datos en el Generador de informes](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md).  
  
  
##  <a name="UpdatingComponents"></a> Actualizar elementos de informe con cambios del servidor  
 Cada vez que abre un informe, el Generador de informes comprueba si las instancias del servidor de elementos de ese informe se han actualizado en el servidor. También comprueba los cambios de los elementos dependientes de elementos de informe, como el conjunto de datos y los parámetros. Si algún elemento de informe publicado o sus dependencias se han actualizado en el servidor, una barra de información del informe muestra el número de elementos actualizados. Puede elegir ver, y aceptar o rechazar las actualizaciones, o bien descartar la barra de información. Si decide ver las actualizaciones, ve una miniatura del elemento de informe, quien realizó la última modificación y cuando tuvo lugar. A continuación, puede aceptar alguno de los elementos actualizados, o todos ellos.  
  
> [!NOTE]  
>  Puede deshabilitar la barra de información y no ser informado si un elemento de informe ha cambiado. Establece esta opción al agregar el elemento de informe a su informe. Aunque haya deshabilitado la barra de información, aún puede comprobar las actualizaciones. Para obtener más información, vea [Buscar o desactivar actualizaciones (Generador de informes y SSRS)](https://msdn.microsoft.com/9c69792d-d7c4-453b-ae2f-6d2d071d8606).  
  
 El Generador de informes busca diferencias entre la fecha de la última actualización del elemento de informe del servidor y la fecha en que usted sincronizó por última vez ese elemento de informe con el servidor. No comprueba la fecha en que modificó el elemento en su informe. Así, el elemento de informe en su informe y el elemento de informe en el servidor podrían ser bastante distintos, pero cuando el Generador de informes comprueba si hay actualizaciones, no encontrará ninguno.  
  
### <a name="accepting-updates"></a>Aceptar las actualizaciones  
 Al aceptar una actualización para un elemento de informe, reemplaza completamente a la copia del elemento de informe existente en su informe. No puede combinar características del elemento de informe con características del elemento de informe publicado en el servidor. Sin embargo, si ha cambiado una de las dependencias del elemento de informe, por ejemplo un conjunto de datos incrustado, el Generador de informes no copia sobre la dependencia que ya está en su informe. Descarga una nueva copia de la dependencia y actualiza el elemento de informe para que señale a la nueva copia.  
  
### <a name="reverting-to-a-previous-version-of-a-report-part"></a>Revertir a una versión anterior de un elemento de informe  
 Si ha cambiado una versión de un elemento en su informe y decide reemplazarla con la versión que está en el servidor, no puede utilizar el cuadro de diálogo **Actualizar** para hacerlo. La actualización solo se puede realizar en elementos de informe que han cambiado en el servidor desde que los descargó.  
  
 Para revertir a la versión en el servidor, no tiene más que eliminar la versión que tiene en su informe y volver a agregarla.  
  
  
##  <a name="RepublishingComponents"></a> Actualizar elementos de informe en el servidor  
 Puede decidir actualizar un elemento de informe existente en el servidor, o publicarlo como un elemento de informe nuevo sin reemplazar el existente. Al actualizar el elemento de informe en el servidor, no se modifican automáticamente las copias del elemento en otros informes. Si otros autores de informes han agregado ese elemento de informe a un informe, se les informa del cambio la próxima vez que abran ese informe. Pueden elegir aceptar sus cambios o no.  
  
 Si decide publicarlo como un nuevo elemento de informe, el Generador de informes le da un nuevo identificador único, que ya no vincula al elemento de informe original.  
  
 Si el conjunto de datos se incrusta en el elemento de informe, cada vez que publique el elemento de informe, el conjunto de datos se mostrará en el cuadro de diálogo **Publicar elementos de informe** . Los conjuntos de datos compartidos no se muestran en el cuadro de diálogo **Publicar elementos de informe** .  
  
  
##  <a name="RptPartsRptDesigner"></a> Trabajar con elementos de informe en el Diseñador de informes  
 Los elementos de informe funcionan de forma algo diferente en el Diseñador de informes en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. En el Diseñador de informes, la publicación es unidireccional: puede publicar un elemento de informe del Diseñador de informes, pero no puede reutilizar un elemento de informe existente en el Diseñador de informes. Para obtener más información, vea [Elementos de informe en el Diseñador de informes &#40;SSRS&#41;](../../reporting-services/report-design/report-parts-in-report-designer-ssrs.md).  
  
##  <a name="HowTo"></a> Temas de procedimientos  
 [Publicar y volver a publicar elementos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/publish-and-republish-report-parts-report-builder-and-ssrs.md)  
  
 [Buscar elementos de informe y establecer una carpeta predeterminada &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs.md)  
  
 [Buscar o desactivar actualizaciones (Generador de informes y SSRS)](https://msdn.microsoft.com/9c69792d-d7c4-453b-ae2f-6d2d071d8606)  
  
## <a name="see-also"></a>Consulte también  
 [Elementos de informe y conjuntos de datos en el Generador de informes](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md)   
 [Solucionar problemas de elementos de informe (Generador de informes y SSRS)](https://msdn.microsoft.com/d9fe1932-46e7-421b-a8a9-4c54d9576e94)   
 [Administrar elementos de informe](../../reporting-services/report-design/managing-report-parts.md)  
  
  
