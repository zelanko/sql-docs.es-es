---
title: Crear una ubicación de confianza para los sitios de PowerPivot en administración central | Microsoft Docs
ms.custom: ''
ms.date: 11/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a666f365-cd93-43a3-9d3d-e429dfc19b66
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6c5dd66b72ff280431d29ae292af8fa1402095dc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "74684082"
---
# <a name="create-a-trusted-location-for-powerpivot-sites-in-central-administration"></a>Crear una ubicación de confianza para los sitios PowerPivot en Administración central
  Servicios de Excel permite especificar qué ubicaciones son repositorios válidos para los libros que se abren en un servidor de SharePoint. Estas ubicaciones se denominan 'ubicaciones de confianza' y puede utilizar opciones de configuración diferentes para cada ubicación de confianza que cree. En una implementación de PowerPivot para SharePoint, podría considerar crear una ubicación de confianza para los sitios que contienen libros PowerPivot. de modo que pueda aplicar la configuración que funcione mejor para el acceso a datos PowerPivot, al tiempo que conserva la configuración predeterminada para el resto de la granja.  
  
  
  
## <a name="prerequisites"></a>Prerrequisitos  
 Debe ser administrador de servicios o de una granja para designar una dirección URL como una ubicación de confianza.  
  
 Debe conocer la dirección URL del sitio de SharePoint que contiene la Galería de PowerPivot u otra biblioteca que almacene los libros. Para obtener la dirección, abra el sitio que contiene la biblioteca, haga clic con el botón secundario en **Galería de PowerPivot**, seleccione **propiedades**y, a continuación, copie la primera parte de la dirección (URL) que contiene el nombre del servidor y la ruta de acceso del sitio.  
  
##  <a name="overview"></a>Información general del <a name="overview"></a>  
 Una instalación inicial de Servicios de Excel especifica 'http://' como su ubicación de confianza, lo que significa que los libros de cualquier sitio de la granja se pueden abrir en el servidor. Si requiere un control más estrecho sobre las ubicaciones que se consideren de confianza, puede crear nuevas ubicaciones de confianza que se asignen a sitios concretos de una granja y, a continuación, variar la configuración y los permisos de cada una.  
  
 Crear una nueva ubicación de confianza para los sitios que hospedan los libros PowerPivot es especialmente útil si desea conservar los valores predeterminados para el resto de la granja, mientras aplica valores diferentes que funcionan mejor para el acceso a datos PowerPivot. Por ejemplo, una ubicación de confianza que esté optimizada para los libros PowerPivot podría tener un tamaño de libro máximo de 50 MB, mientras que el resto de la granja utiliza el valor predeterminado de 10 MB.  
  
 Se recomienda crear una ubicación de confianza si está utilizando las bibliotecas de Galerías de PowerPivot para ofrecer una vista previa de los libros publicados y encuentra advertencias en la actualización de datos en lugar de la imagen de la vista previa que esperaba. La Galería de PowerPivot representa imágenes en miniatura de los informes y los libros utilizando los datos y la información de la presentación dentro del documento. Si la opción Avisar al actualizar está habilitada para una ubicación de confianza, la Galería de PowerPivot podría no tener los permisos necesarios para realizar la actualización, con lo que aparecería un error en lugar de la imagen en miniatura. Si se agrega un sitio que contiene la Galería de PowerPivot como una nueva ubicación de confianza, es posible que se elimine este problema.  
  
##  <a name="create-a-trusted-location-for-powerpivot-data-access"></a><a name="create"></a>Crear una ubicación de confianza para el acceso a datos PowerPivot  
  
1.  En Administración central, en Administración de aplicaciones, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Haga clic en la aplicación de servicio de Servicios de Excel.  
  
3.  Haga clic en **Ubicaciones de archivos de confianza**.  
  
4.  Haga clic en **Agregar ubicación de archivo de confianza**.  
  
5.  Escriba la dirección URL de un sitio que contenga una biblioteca de la Galería de PowerPivot.  
  
6.  En Tipo de ubicación, seleccione **Microsoft SharePoint Foundation**.  
  
    > [!IMPORTANT]  
    >  Los tipos de ubicación HTTP y UNC no se admiten para el acceso a datos PowerPivot.  
  
7.  Acepte toda la configuración predeterminada para las propiedades de Administración de sesiones, Propiedades del libro y Comportamiento del cálculo.  
  
8.  En Propiedades del libro, establezca **Tamaño máximo del libro** en **50**. De esta forma, se alinea el límite superior del tamaño de archivo al límite superior para las cargas de archivo en la aplicación del sitio web principal. Si los libros son mayores de 50 megabytes, debe aumentar el límite del tamaño de archivo. Para obtener más información, vea [configurar el tamaño máximo de carga de archivos &#40;PowerPivot para SharePoint&#41;](configure-maximum-file-upload-size-power-pivot-for-sharepoint.md).  
  
9. En Datos externos, compruebe que Permitir datos externos está establecido en **Bibliotecas de conexiones de datos de confianza e incrustadas**. Este valor se requiere para el acceso a datos PowerPivot en un libro.  
  
10. Además, en Datos externos, en Avisar al actualizar, desactive la casilla de **Advertencia de actualización habilitada**. Al desactivar la casilla, se permite que la Galería de PowerPivot omita los mensajes de advertencia rutinarios y muestre imágenes de vista previa de un libro en su lugar.  
  
11. Haga clic en **OK**.  
  
## <a name="see-also"></a>Consulte también  
 [Galería de PowerPivot](../../2014-toc/index.yml)  
 [Crear y personalizar la galería de PowerPivot](create-and-customize-power-pivot-gallery.md)   
 [Usar la galería de PowerPivot](use-power-pivot-gallery.md)  
  
  
