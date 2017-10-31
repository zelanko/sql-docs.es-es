---
title: Vistas previas de informes en el generador de informes | Documentos de Microsoft
ms.custom: 
ms.date: 01/09/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ba6b5bdd-d8c6-4aa8-ba32-3a10b11969d4
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 1635c00223ae559c703a56e528f8e4f74f5a67ef
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="previewing-reports-in-report-builder"></a>Mostrar la vista previa de informes en el Generador de informes
  Durante la creación de un informe paginado de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , resulta útil obtener una vista previa del mismo a menudo para comprobar que muestra lo que se pretende. Para obtener una vista previa de un informe, haga clic en **Ejecutar**. El informe se representa en el modo de vista previa.  
  
 El Generador de informes mejora la experiencia de vista previa utilizando sesiones de edición cuando se conecta a un servidor de informes. La sesión de edición crea una memoria caché de datos y hace que los conjuntos de datos de la memoria caché estén disponibles para las diferentes vistas previas del informe. Una sesión de edición no es una característica con la que se interactúe directamente, pero saber cuándo se actualiza el conjunto de datos almacenado en memoria caché le ayudará a mejorar el rendimiento al obtener una vista previa de un informe y saber por qué el informe se representa con más rapidez o lentitud.  
  
 Otras ventajas de las sesiones de edición son las funciones para modificar los informes que usan orígenes de datos incrustados o hacen referencia a elementos, como imágenes o subinformes, que están almacenados en el servidor de informes.  
  
> [!NOTE]  
> Hay algunas diferencias entre una vista previa en el generador de informes y ver en un explorador. Por ejemplo, un control de calendario, que se agrega a un informe cuando se especifica un parámetro de tipo de fecha y hora, es diferente en el generador de informes y en un explorador. 
  
## <a name="improving-preview-performance"></a>Mejorar el rendimiento de las vistas previas  
 El modo en que se crean y actualizan los informes afecta a la rapidez con que se representan en la vista previa. La primera vez que obtiene una vista previa de un informe que se basa en una referencia del servidor, se crea automáticamente una sesión de edición y los datos que se usan cuando se ejecuta el informe se agregan a una memoria caché de datos que está almacenada en el servidor de informes. Al efectuar cambios en el informe que no afectan a los datos, el informe utiliza la copia de los datos que está en la memoria caché. Esto significa que no verá el cambio de los datos cada vez que obtenga una vista previa del informe. Si desea los nuevos datos, haga clic en el botón **Actualizar** en la cinta de opciones.  
  
 Las acciones siguientes hacen que la memoria caché se actualice y ralentizan la representación del informe la próxima vez que se obtenga una vista previa del mismo:  
  
-   Agregar, cambiar o eliminar un conjunto de datos. El conjunto de datos almacenado en memoria caché contiene todos los conjuntos de datos que un informe utiliza y la modificación de cualquier conjunto de datos invalida el conjunto de datos almacenado en memoria caché. Esto incluye cambiar el nombre, la consulta o los campos en el conjunto de datos.  
  
    > [!NOTE]  
    >  Si el conjunto de datos tiene un número grande de campos que no espera utilizar, debería considerar actualizarlo para omitir esos campos. Aunque esto crea una nueva sesión de edición y la primera vista previa del informe es más lenta, el menor conjunto de datos almacenado en memoria caché resulta beneficioso en conjunto para el rendimiento del servidor de informes.  
  
-   Agregar, cambiar o eliminar un origen de datos. Esto incluye cambiar el nombre o las propiedades del origen de datos, la extensión de datos del origen de datos o las propiedades de la conexión con el origen de datos.  
  
-   Cambiar el origen de datos compartido que el informe utiliza por otro origen de datos diferente.  
  
-   Cambiar el idioma del informe.  
  
-   Cambiar los ensamblados o el código personalizado que el informe utiliza.  
  
-   Agregar, cambiar o eliminar los parámetros de la consulta en los valores de parámetros o informes.  
  
 Los cambios del diseño de informe y del formato de los datos no afectan al conjunto de datos almacenado en memoria caché. Puede efectuar las acciones siguientes sin actualizar el conjunto de datos almacenado en memoria caché:  
  
-   Agregar o quitar regiones de datos como tablas, matrices o gráficos.  
  
-   Agregar o eliminar columnas del informe. Todos los campos del conjunto de datos están disponibles para utilizarlos en el informe. Agregar o quitar campos en el informe no tiene ningún efecto en el conjunto de datos.  
  
-   Cambiar el orden de los campos en las tablas y matrices.  
  
-   Agregar, cambiar o eliminar grupos de filas y columnas.  
  
-   Agregar, cambiar o eliminar el formato de los valores de datos en los campos.  
  
-   Agregar, cambiar o eliminar imágenes, líneas o cuadros de texto.  
  
-   Cambiar los saltos de página.  
  
 La sesión de edición se crea la primera vez que se obtiene una vista previa de un informe. De forma predeterminada, una sesión de edición dura 7.200 segundos (2 horas). La sesión se restablece en dos horas cada vez que se ejecuta el informe. Cuando la sesión de edición expira, se elimina la memoria caché de datos. Si la sesión de edición expira, se vuelve a crear una automáticamente la próxima vez que se obtiene una vista previa del informe. El tiempo de expiración para las sesiones de edición se puede configurar. Si encuentra que dos horas es un período de tiempo demasiado largo o demasiado corto, póngase en contacto con el administrador del servidor de informes.  
  
 De forma predeterminada, la memoria caché de datos puede contener hasta cinco conjuntos de datos. Si utiliza muchas combinaciones diferentes de valores de parámetros, el informe podría necesitar más datos. Esto requiere que la memoria caché se actualice y el informe se represente más lentamente la próxima vez que se obtenga una vista previa del mismo. El administrador del servidor de informes puede configurar el número de entradas en la memoria caché.  
  
## <a name="concurrency-of-report-updates"></a>Simultaneidad de las actualizaciones de informes  
 Con frecuencia, se obtiene una vista previa de un informe como paso para actualizarlo y guardarlo después en un servidor de informes. Cuando actualiza un informe, es posible que alguien más lo esté actualizando y lo guarde después al mismo tiempo. El informe que se guarda en último lugar es la versión del informe que está disponible para su posterior consulta y actualización. Podría darse el caso de que la versión del informe de la que obtuvo una vista previa no sea la versión que vuelve a abrir posteriormente. Tiene la opción de guardar el informe con un nombre nuevo utilizando la opción **Guardar como** en el menú del Generador de informes.  
  
## <a name="external-report-items"></a>Elementos de informe externos  
 Un informe puede incluir elementos como orígenes de datos compartidos, imágenes externas y subinformes que se almacenan de forma independiente del informe. Dado que los elementos se almacenan independientemente, es posible que se puedan eliminar o mover a una ubicación diferente en el servidor de informes. Si ocurre esto, podría no obtenerse una vista previa del informe. Puede actualizar el informe para indicar la ubicación actualizada del elemento o si el elemento se eliminó, reemplazarlo por un elemento existente o quitar la referencia al mismo desde el informe.  
  
 Si el subinforme utilizado por el informe cambia una vez creada la sesión de edición, este no se representará en la vista previa. Para obtener correctamente una vista previa del informe, debe guardarlo o hacer clic en **Actualizar** para obtener los datos nuevos.  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de datos de informe &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [Aplicar formato a elementos de informe &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [Tablas, Matrices y listas de &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Gráficos &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Tablas, Matrices y listas de &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Guardar informes &#40; El generador de informes &#41;](../../reporting-services/report-builder/saving-reports-report-builder.md)  
  
  

