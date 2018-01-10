---
title: Trabajar con conjuntos de datos compartidos (portal web) | Microsoft Docs
ms.custom: 
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2641ea84-9343-4e6f-aec1-25339031b163
caps.latest.revision: "7"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4e72c48f816752530abddb6246410e4936ac20a6
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2018
---
# <a name="work-with-shared-datasets---web-portal"></a>Trabajar con conjuntos de datos compartidos: portal web

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

Con un conjunto de datos compartido, puede administrar los valores para un conjunto de datos de forma independiente de los informes y otros elementos de catálogo que lo utilizan. Los conjuntos de datos compartidos pueden usarse con informes paginados y móviles, junto con los KPI.

Puede ver y administrar las propiedades de un conjunto de datos compartido en el portal web. El portal web puede iniciar el Generador de informes para crear o editar conjuntos de datos compartidos.

## <a name="create-a-shared-dataset"></a>Creación de un conjunto de datos compartido
  
Para crear un nuevo conjunto de datos compartido, puede hacer lo siguiente:  
  
1.  Seleccione Nuevo en la barra de menús.  
  
2.  Seleccione **Conjunto de datos**.  
  
    ![ssRSDataset-NewDataset](../reporting-services/media/ssrsdataset-newdataset.png)  
  
3.  Se iniciará el Generador de informes o se le pedirá que lo descargue.  
  
4.  En el cuadro de diálogo **Nuevo informe o conjunto de datos** , seleccione la conexión de origen de datos que se utilizará para este conjunto de datos. Puede que deba buscar la ubicación del origen de datos compartido.  
  
5.  Seleccione **Crear**.  
  
6.  Cree el conjunto de datos y, después, seleccione el icono de **guardado** situado en la esquina superior izquierda para guardarlo en el servidor de informes.  
  
## <a name="manage-an-existing-shared-dataset"></a>Administración de un conjunto de datos compartido existente
  
Para administrar un conjunto de datos compartido existente, puede hacer lo siguiente:  
  
> [!NOTE]
> Si no ve el conjunto de datos compartido en la carpeta, asegúrese de que está viendo conjuntos de datos. Puede seleccionar **Ver** en la barra de menús de la esquina superior derecha del portal web. Asegúrese de que la casilla **Conjuntos de datos** está activada.  
  
1.  Haga clic en los **puntos suspensivos (…)** del conjunto de datos que quiere administrar.  
  
    ![ssRSDataset-Ellipse](../reporting-services/media/ssrsdataset-ellipse.png)  
  
2.  Seleccione **Administrar**, que le llevará a la pantalla de edición.  
  
    ![ssRSDataset-Manage](../reporting-services/media/ssrsdataset-manage.png)  
  
## <a name="properties"></a>Propiedades
  
En la pantalla de propiedades, puede cambiar el **nombre** y la **descripción** del conjunto de datos. También puede **Eliminar**, **Mover**, **Editar en el Generador de informes**, **Descargar** o **Reemplazar**.  
  
![ssRSdataset-Properties](../reporting-services/media/ssrsdataset-properties.png)  
  
## <a name="caching"></a>Almacenamiento en memoria caché
  
Dispone de varias opciones para almacenar en memoria caché los datos de un conjunto de datos. Puede empezar con una selección simple.  
  
1.  **Ejecutar este informe siempre con los datos más recientes** emitirá consultas al origen de datos cuando se solicite.  
  
2.  **Cache copies of this report and use them when available** (Almacenar en caché copias del informe y usarlas cuando estén disponibles) colocará una copia temporal de los datos en una memoria caché para su uso con elementos que utilicen este conjunto de datos. El almacenamiento en memoria caché suele mejorar el rendimiento porque los datos se devuelven desde la memoria caché en lugar de ejecutarse de nuevo la consulta del conjunto de datos.  
  
![ssRSDataset-Caching1](../reporting-services/media/ssrsdataset-caching1.png)  
  
Si selecciona **Cache Copies of this report and use them when available** (Almacenar en caché copias del informe y usarlas cuando estén disponibles), dispondrá de más opciones.  
  
![ssRSDataset-Caching2](../reporting-services/media/ssrsdataset-caching2.png)  
  
### <a name="cache-expiration"></a>Expiración de la caché  
  
Puede controlar si desea que la caché expire, para el conjunto de datos compartido, después de una cantidad de tiempo determinada, o bien si prefiere hacerlo según una programación. Puede usar una programación compartida.  
  
![ssRSDataset-Caching3](../reporting-services/media/ssrsdataset-caching3.png)  
  
> [!NOTE]
> La memoria caché no se actualiza al establecer una expiración. Sin un plan de actualización de caché, los datos se actualizarán con la siguiente ejecución del conjunto de datos.  
  
### <a name="cache-refresh-plans"></a>Planes de actualización de caché  
  
Puede utilizar planes de actualización de caché a fin de crear programaciones para cargar previamente la caché con copias temporales de datos de un conjunto de datos compartido. Un plan de actualización incluye una programación y la opción para especificar o invalidar los valores de los parámetros. No puede invalidar los valores de los parámetros que estén marcados como de solo lectura. Puede crear y utilizar más de un plan de actualización.   
  
Las asignaciones de roles predeterminadas que permiten agregar, eliminar y cambiar los conjuntos de datos compartidos para los planes de actualización de caché son Administrador de contenido, Mis informes y Publicador.  
  
Después de aplicar la opción de caché anterior, puede definir el plan de actualización de caché. Para ello, seleccione el vínculo **Manage Refresh Plans** (Administrar planes de actualización) que aparecerá tras aplicar la configuración de la caché. Se le llevará a la página de planes de actualización de caché.   
  
Para crear un nuevo plan de actualización de caché, seleccione **Nuevo plan de actualización de caché**. Después, puede escribir un nombre para el plan y especificar una programación. Si el conjunto de datos tiene parámetros definidos, verá que se enumeran y podrá especificar valores, a menos que estén marcados como de solo lectura.  
  
Cuando haya terminado, puede seleccionar **Create Cache Refresh Plan**(Crear plan de actualización de caché).  
  
![ssRSDataset-Caching4](../reporting-services/media/ssrsdataset-caching4.png)  
  
> [!NOTE]
> El Agente SQL Server debe estar ejecutándose para poder crear un plan de actualización de caché.  
  
A continuación, puede **editar** o **eliminar** los planes que se muestren. La opción **Nuevo a partir de existente** se habilita cuando solo está seleccionado un plan de actualización de caché. Esta opción creará un plan de actualización nuevo que se copia a partir del plan original. El plan de actualización de caché se abre rellenado de antemano con detalles del plan que se seleccionara. A continuación puede modificar las opciones del plan de actualización y guardar el plan con otra descripción.  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
