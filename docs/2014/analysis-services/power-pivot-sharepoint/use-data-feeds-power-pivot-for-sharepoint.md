---
title: Usar fuentes de distribución de datos (PowerPivot para SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 50140fdf-6fd1-41a1-9c14-8ecfb97ba2e1
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0e974c81b3f65ef7830362bc80fc7f15df0f1009
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37249415"
---
# <a name="use-data-feeds-powerpivot-for-sharepoint"></a>Usar fuentes de distribución de datos (PowerPivot para SharePoint)
  Las fuentes de distribución de datos son una o varias secuencias de datos que se generan en un origen de datos en línea y se difunden en un documento o aplicación de destino. Si está utilizando PowerPivot para Excel, las fuentes de distribución de datos pueden ayudarle a poner los datos empresariales o corporativos existentes de orígenes de datos arbitrarios en la ventana de PowerPivot de un libro de Excel 2010. Después de importar una fuente de distribución de datos en un libro, puede hacer referencia a ella posteriormente en cualquier operación de actualización de datos que programe en un servidor de SharePoint.  
  
 El modo de utilizar una fuente de distribución de datos depende de si se utilizan las características de exportación integradas en las aplicaciones compatibles con las fuentes de distribución de datos de Atom, o si se crean y usan servicios de datos personalizados. Las aplicaciones que pueden publicar y leer los datos XML de Atom permiten una transferencia de datos sin problemas que oculta la mecánica de los servicios de datos y fuentes de distribución de datos a los usuarios. Para un usuario, simplemente mueve los datos de una aplicación a otra.  
  
 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y Microsoft SharePoint 2010 proporcionan fuentes de distribución que se pueden usar en los libros PowerPivot de datos. Puede utilizar la información de este tema para saber cómo tener acceso a las fuentes de distribución de datos de los informes y las listas de que ya disponga.  
  
 Este tema contiene las siguientes secciones:  
  
 [Requisitos previos](#prereq)  
  
 [Crear una fuente de distribución de datos a partir de una lista de SharePoint](#sharepointlist)  
  
 [Crear una fuente de distribución de datos a partir de un informe de Reporting Services](#rsreport)  
  
 [Crear una fuente de distribución de datos a partir de un documento de servicio de datos](#dsdoc)  
  
##  <a name="prereq"></a> Requisitos previos  
 Para importar una fuente de distribución de datos en Excel 2010, debe tener PowerPivot para Excel.  
  
 Debe tener un servicio web o un servicio de datos que proporcione los datos en el formato de Atom 1.0. Tanto [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] como SharePoint 2010 pueden proporcionar los datos en este formato.  
  
 Antes de poder exportar una lista de SharePoint como una fuente de distribución de datos, debe instalar ADO.NET Data Services en el servidor de SharePoint. Para obtener más información, vea [Instalar ADO.NET Data Services para admitir las exportaciones de fuentes de distribución de datos de las listas de SharePoint](../../sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md).  
  
##  <a name="sharepointlist"></a> Crear una fuente de distribución de datos a partir de una lista de SharePoint  
 En una granja de SharePoint 2010, una lista de SharePoint tiene un botón Exportar como fuente de distribución de datos en la cinta de opciones Lista. Puede hacer clic en este botón para exportar la lista como una fuente. Para obtener los mejores resultados, debería tener Excel 2010 con la aplicación cliente de PowerPivot en la estación de trabajo. La aplicación cliente de PowerPivot se iniciará en respuesta a la exportación de la fuente de distribución de datos y creará una nueva tabla de PowerPivot que contenga la lista.  
  
1.  Abra la lista en el sitio de SharePoint.  
  
2.  En Herramientas de lista, haga clic en **Lista**.  
  
3.  En Conectar y exportar, haga clic en **Exportar como fuente de distribución de datos**.  
  
    > [!NOTE]  
    >  El **exportar como fuente de distribución de datos** botón se agrega a SharePoint por medio de PowerPivot. Si no tiene PowerPivot para SharePoint instalado o no activó la característica PowerPivot, este botón no estará disponible.  
  
4.  Haga clic en **abierto** si PowerPivot para Excel está instalado localmente, o haga clic en **guardar** para guardar el documento .atomsvc en el disco duro para las operaciones de importación en un momento posterior.  
  
5.  Si elige **Abrir**, use el Asistente para la importación de tablas a fin de importar la fuente de distribución de datos en una hoja de cálculo. La fuente de distribución de datos se agregará como una nueva tabla en la ventana de PowerPivot.  
  
 Se producirá un error si ADO.NET Data Services 3.5.1 no está instalado en el servidor de SharePoint. Para obtener más información sobre el error y cómo resolverlo, consulte [Instalar ADO.NET Data Services para admitir las exportaciones de fuentes de distribución de datos de las listas de SharePoint](../../sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md).  
  
##  <a name="rsreport"></a> Crear una fuente de distribución de datos a partir de un informe de Reporting Services  
 Si tiene una implementación de Reporting Services de SQL Server 2008 R2, puede usar la nueva extensión de representación de Atom para generar una fuente de distribución de datos a partir de un informe existente. Para obtener los mejores resultados, debería tener Excel 2010 con PowerPivot para Excel en la estación de trabajo. La aplicación cliente de PowerPivot se iniciará en respuesta a la exportación de la fuente de datos, y agregará y relacionará las tablas y columnas automáticamente a medida que se transmitan.  
  
 Para obtener instrucciones sobre cómo exportar una fuente de distribución de datos a partir de un informe, vea [Generar fuentes de distribución de datos a partir de un informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/generate-data-feeds-from-a-report-report-builder-and-ssrs.md) en el [archivo de Ayuda del Generador de informes](http://go.microsoft.com/fwlink/?LinkId=154494).  
  
> [!NOTE]  
>  Para configurar la programación de una actualización de datos reiterada que vuelva a importar los datos del informe en un libro PowerPivot que esté publicado en una biblioteca de SharePoint, el servidor de informes se debe configurar para la integración de SharePoint. Para obtener más información sobre el uso de PowerPivot para SharePoint y Reporting Services juntos, consulte [configuración y administración de un servidor de informes &#40;Reporting Services SharePoint Mode&#41;](../../reporting-services/configure-administer-report-server-reporting-services-sharepoint-mode.md).  
  
##  <a name="dsdoc"></a> Crear una fuente de distribución de datos a partir de un documento de servicio de datos  
 Si tiene un servicio de datos personalizado que genera las fuentes Atom, puede configurar un documento de servicio de datos para hacer que los datos estén disponibles para los usuarios y aplicaciones. Un archivo de *documento de servicio de datos* (.atomsvc) especifica una o varias conexiones a los orígenes en línea que publican los datos en el formato de conexión de Atom. Los documentos de servicio de datos se pueden crear en una *biblioteca de fuente de distribución de datos*, que es una biblioteca con una finalidad especial que proporciona un punto de acceso común para examinar los documentos de servicio de datos publicados en un servidor de SharePoint. Los trabajadores de la información que disponen de permiso de acceso a los documentos de servicio de datos en la biblioteca de fuentes de distribución de datos pueden hacer referencia a la dirección URL de SharePoint del documento para importar las fuentes de distribución de datos en sus libros y aplicaciones.  
  
1.  Abra una biblioteca de fuentes de distribución de datos que creara el administrador del sitio. Para obtener más información, consulte [crear o personalizar una biblioteca de fuentes de distribución de datos &#40;PowerPivot para SharePoint&#41;](create-or-customize-a-data-feed-library-power-pivot-for-sharepoint.md).  
  
2.  En las herramientas de biblioteca, haga clic en **Documentos**.  
  
3.  Haga clic en **Nuevo documento**.  
  
4.  Proporcione un nombre de archivo y una descripción.  
  
5.  Especifique una o más direcciones URL que proporcionen la fuente:  
  
    1.  La**Dirección URL base** es opcional. Debería especificarla si un documento de servicio de datos proporciona varias fuentes. La dirección URL base debería especificar la parte de la dirección URL que sea común a todas las fuentes (por ejemplo, el nombre del servidor y el sitio). Si está creando un documento de servicio de datos para un informe de Reporting Services, la dirección URL base sería la dirección URL del servidor de informes y el informe.  
  
    2.  La**Dirección URL del servicio web** es obligatoria. Sin la dirección URL base, este valor debe incluir http:// o https:// en la dirección. Si especificó una dirección URL base, la dirección URL del servicio web es la parte que sigue a la dirección URL base. Por ejemplo, si la dirección URL completa es http://adventure-works/inventory/today.aspx, la dirección URL Base sería http://adventure-works/inventory, y la dirección URL del servicio Web sería/Today.aspx.  
  
         La dirección URL del servicio web puede incluir parámetros que filtran o seleccionan un subconjunto de datos. La aplicación o servicio que proporciona la fuente debe admitir los parámetros que especifique en la dirección URL.  
  
6.  Escriba un **Nombre de tabla**y una tabla para cada fuente. Este valor es necesario. La aplicación cliente que utilice la fuente de distribución de datos usa el nombre de tabla. En PowerPivot para Excel, el nombre de tabla se utiliza para denominar las tablas en la ventana de PowerPivot que contendrá los datos importados.  
  
## <a name="see-also"></a>Vea también  
 [Activar la integración de características de PowerPivot para colecciones de sitios en Administración Central](activate-power-pivot-integration-for-site-collections-in-ca.md)   
 [Compartir las fuentes de datos mediante una biblioteca de fuentes de datos &#40;PowerPivot para SharePoint&#41;](share-data-feeds-using-a-data-feed-library-power-pivot-for-sharepoint.md)  
  
  
