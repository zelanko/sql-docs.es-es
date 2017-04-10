---
title: "Crear o personalizar una biblioteca de fuentes de distribuci&#243;n de datos (PowerPivot para SharePoint) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "biblioteca de fuentes de distribución de datos"
  - "fuentes de distribución de datos (Analysis Services con SharePoint]"
ms.assetid: 699fbeb9-42ab-436b-beba-214db51ea3dd
caps.latest.revision: 22
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 22
---
# Crear o personalizar una biblioteca de fuentes de distribuci&#243;n de datos (PowerPivot para SharePoint)
  Una *biblioteca de fuentes de distribución de datos* es una biblioteca de SharePoint especial que le permite registrarse y compartir los documentos (.atomsvc) de servicio de datos de Atom. En estos documentos se proporcionan fuentes de distribución de datos XML para libros [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] u otras aplicaciones cliente que admitan el formato de distribución de datos Atom. Una biblioteca de fuentes de distribución de datos es diferente de otras bibliotecas de SharePoint porque permite:  
  
-   Crear o modificar un *documento de servicio de datos*, que se usa para especificar una conexión HTTP a una fuente concreta.  
  
-   Compartir y administrar los documentos de servicio de datos en una ubicación central.  
  
-   Identificar visualmente los documentos de servicio de datos mediante un icono, para que pueda distinguir con facilidad los documentos de servicio de otros documentos almacenados en la misma biblioteca: ![GMNI_IconDataFeed](../../analysis-services/power-pivot-sharepoint/media/gmni-icondatafeed.png "GMNI_IconDataFeed")  
  
 Una biblioteca de fuentes de distribución de datos siempre contiene archivos de documentos de servicio de datos (.atomsvc) y nunca las propias fuentes de distribución de datos. A diferencia de una fuente de distribución de datos, que consta de datos XML estáticos, el documento de servicio de datos especifica una dirección URL para un servicio o aplicación que genera una fuente tras la solicitud, proporcionando información de conexión reutilizable para las operaciones de importación repetibles.  
  
 Este tema contiene las siguientes secciones:  
  
 [Requisitos previos](#prereq)  
  
 [Crear una nueva biblioteca de fuentes de distribución de datos](#createlib)  
  
 [Agregar el tipo de contenido de la fuente de distribución de datos a una biblioteca](#addtolib)  
  
##  <a name="prereq"></a> Requisitos previos  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] se debe activar para los sitios para los que vaya a crear la biblioteca de fuentes de distribución de datos. Si el tipo de plantilla de biblioteca de fuentes de distribución de datos no está disponible, probablemente se deba a que no se ha cumplido este requisito previo. Para más información, consulte [Activate Power Pivot Feature Integration for Site Collections in Central Administration](../../analysis-services/power-pivot-sharepoint/activate power pivot integration for site collections in ca.md).  
  
 Debe ser propietario del sitio para crear la biblioteca.  
  
##  <a name="createlib"></a> Crear una nueva biblioteca de fuentes de distribución de datos  
 Crear una biblioteca de fuentes de distribución de datos es el primer paso si se desea habilitar fuentes de distribución de datos para los libros de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Dado que una biblioteca de fuentes de distribución de datos proporciona las páginas de aplicación y administración para los documentos de servicio de datos, debe disponer de una para poder crear un documento nuevo.  
  
 Una biblioteca de fuentes de distribución de datos se basa en una plantilla integrada y en un *tipo de contenido del documento de servicio de datos* preconfigurado que define las propiedades y comportamientos para un documento de servicio de datos.  
  
1.  Haga clic en **Acciones de sitio** en la esquina superior izquierda de la página.  
  
2.  Haga clic en **Más opciones**...  
  
3.  En Bibliotecas, haga clic en **Biblioteca de fuentes de distribución de datos**.  
  
4.  Escriba el nombre, la descripción y las preferencias de la versión e inicio. Incluya información descriptiva que ayude a los usuarios a identificar esta biblioteca como almacenamiento para los documentos de servicio de datos.  
  
5.  Haga clic en **Crear**.  
  
 Un vínculo a la biblioteca de fuentes de distribución de datos aparecerá en el panel Inicio rápido de navegación para el sitio actual.  
  
 Después de crear una biblioteca, puede utilizarla para crear documentos de servicio de datos. Para más información, vea [Uso de fuentes de distribución de datos &#40;PowerPivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/use-data-feeds-power-pivot-for-sharepoint.md).  
  
##  <a name="addtolib"></a> Agregar el tipo de contenido de la fuente de distribución de datos a una biblioteca  
 Si no desea crear una biblioteca de fuentes de distribución de datos dedicada, pero sigue deseando crear y administrar los documentos de servicio de datos desde un sitio de SharePoint, puede agregar y configurar manualmente el tipo de contenido del documento de servicio de datos para cualquier biblioteca que use para compartir los archivos de documento de servicio de datos (.atomsvc).  
  
 Para agregar y configurar un tipo de contenido, debe tener al menos el permiso Administrar listas. Este permiso se integra en el nivel de permisos de diseño y superiores.  
  
 Los siguientes pasos se deben repetir para cada biblioteca en la que desee crear o modificar los documentos de registro de fuentes de distribución de datos.  
  
#### Paso 1: habilitar la administración de tipos de contenido  
  
1.  Abra la biblioteca de documentos para la que desee habilitar varios tipos de contenido.  
  
2.  En la cinta de opciones de SharePoint, en Herramientas de biblioteca, haga clic en **Biblioteca**.  
  
3.  Haga clic en **Configuración**.  
  
4.  Haga clic en **Configuración de la biblioteca**.  
  
5.  En Configuración general, haga clic en **Configuración avanzada**.  
  
6.  En Tipos de contenido, en la sección "¿Desea permitir la administración de tipos de contenido?" haga clic en **Sí**.  
  
7.  Haga clic en **Aceptar**.  
  
#### Paso 2: agregar el tipo de contenido de documento de servicio de datos  
  
1.  En la sección Tipos de contenido, haga clic en **Agregar a partir de tipos de contenido de sitio**. Si no ve esta página, regrese al sitio, haga clic en **Biblioteca** en Herramientas de biblioteca y, a continuación, haga clic en **Configuración de la biblioteca**.  
  
2.  En Tipos de contenido, haga clic en **Agregar a partir de tipos de contenido de sitio**.  
  
3.  En Seleccionar tipos de contenido de sitio de:, seleccione **Business Intelligence**.  
  
4.  En la lista Tipos de contenido de sitio disponibles, haga clic en **Documento de servicio de datos**y, a continuación, haga clic en **Agregar** para mover el tipo de contenido seleccionado a la lista Tipos de contenido que agregar.  
  
5.  Haga clic en **Aceptar**.  
  
#### Paso 3: comprobar la configuración del documento de servicio de datos  
  
1.  Abra la página principal del sitio.  
  
2.  Abra la biblioteca.  
  
3.  En la cinta de opciones de SharePoint, haga clic en **Documentos**.  
  
4.  Haga clic en la flecha abajo en Nuevo documento y seleccione **Documento de servicio de datos**. Debería aparecer la página Nuevo documento de servicio de datos.  
  
## Vea también  
 [Uso de fuentes de distribución de datos &#40;PowerPivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/use-data-feeds-power-pivot-for-sharepoint.md)   
 [Eliminar una biblioteca de fuente de distribución de datos Power Pivot](../../analysis-services/power-pivot-sharepoint/delete-a-power-pivot-data-feed-library.md)   
 [Administración y configuración del servidor de Power Pivot en Administración central](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [Fuentes de distribución de datos de PowerPivot](../../analysis-services/power-pivot-sharepoint/power-pivot-data-feeds.md)  
  
  