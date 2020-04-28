---
title: Tipo de conexión de PowerPivot (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a104c3c7-f118-4d02-9a0f-6859f1469d11
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 50ce060d270cf06a771136c581bf96fe1ec21eee
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "79112146"
---
# <a name="powerpivot-connection-type-ssrs"></a>Tipo de conexión de PowerPivot (SSRS)
  Puede utilizar la extensión de procesamiento de datos de SQL Server Analysis Services para recuperar datos de un libro PowerPivot publicado en una galería de PowerPivot de SharePoint.  
  
 Utilice la información de este tema para crear un origen de datos. Para obtener instrucciones paso a paso, vea [Agregar y comprobar una conexión de datos o un origen de datos &#40;generador de informes y SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 El origen de datos PowerPivot se debe publicar en una galería de PowerPivot en un sitio de SharePoint.  
  
 Para admitir conexiones del Generador de informes con un libro PowerPivot, debe tener SQL Server 2008 R2 ADOMD.NET en su equipo en la estación de trabajo. Esta biblioteca cliente se instala con PowerPivot para Excel, pero si está usando un equipo que no tiene esta aplicación, debe descargar e instalar ADOMD.NET de la página [Microsoft SQL Server 2008 R2 Feature Pack](https://www.microsoft.com/download/details.aspx?id=44272).  
  
## <a name="data-source-type"></a>Tipo de origen de datos  
 Utilice el origen de datos de informe de tipo **Microsoft SQL Server Analysis Services**.  
  
## <a name="connection-string"></a>Cadena de conexión  
 La cadena de conexión es la dirección URL del libro PowerPivot publicado en SharePoint en la galería de PowerPivot u otra biblioteca, http://contoso-srv/subsite/PowerPivotLibrary/ContosoSales.xlsxpor ejemplo,.  
  
## <a name="credentials"></a>Credenciales  
 Especifique las credenciales necesarias para tener acceso al libro PowerPivot y el sitio de SharePoint, por ejemplo, Autenticación de Windows (Seguridad integrada). Para obtener más información, vea [conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) o [Especifique las credenciales en generador de informes](../specify-credentials-in-report-builder.md).  
  
## <a name="queries"></a>Consultas  
 Cuando esté conectado al origen de datos PowerPivot, utilice el diseñador gráfico de consultas MDX para crear una consulta examinando las estructuras de datos subyacentes y seleccionando una de ellas. Después de generar una consulta, ejecútela para ver los datos de muestra en el panel de resultados.  
  
 El diseñador de consultas analiza la consulta para determinar los campos del conjunto de datos. También puede modificar manualmente la colección de campos del conjunto de datos en el panel **Datos de informe** . Para obtener más información, consulte [Agregar, editar y actualizar campos en el panel Datos de informe &#40;Generador de informes y SSRS&#41;](add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md).  
  
## <a name="filters"></a>Filtros  
 En el recuadro Filtros, especifique dimensiones y miembros para excluirlos o incluirlos en los resultados de la consulta.  
  
## <a name="parameters"></a>Parámetros  
 En el panel Filtros, seleccione la opción **Parámetros** para que un filtro cree automáticamente un parámetro de informe con valores disponibles que correspondan a las selecciones de filtro.  
  
## <a name="remarks"></a>Observaciones  
 Si abre el Generador de informes desde el libro PowerPivot en una Galería de PowerPivot, las tablas dinámicas, gráficos dinámicos, segmentaciones de datos, y otras características analíticas y de diseño del libro PowerPivot no se vuelven a crear en el informe. En lugar de ello, el informe en blanco contiene un origen de datos preconfigurado que selecciona los datos del libro PowerPivot. El diseño de informes basados en un libro PowerPivot puede ser laborioso y lento, dependiendo del número de segmentaciones de datos, filtros y tablas o gráficos que desee crear en el informe. Resulta más práctico imaginar la presentación de los datos deseados en un informe independientemente de diseño existente en PowerPivot.  
  
 Los datos de un libro PowerPivot están muy comprimidos. Los datos recuperados del libro PowerPivot para crear un informe no están comprimidos. Use el diseñador de consultas para especificar filtros y parámetros con el fin de limitar los datos a los estrictamente necesarios en el informe.  
  
 A diferencia de la conexión a un cubo de Analysis Services, un modelo de PowerPivot no tiene jerarquías. Para proporcionar una funcionalidad similar a las segmentaciones de datos relacionadas del libro, debe crear colocando parámetros en cascada en el informe. Para más información, vea [Agregar parámetros en cascada a un informe &#40;Generador de informes y SSRS&#41;](../report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md).  
  
 En algunos casos, podría necesitar ajustar las expresiones para aceptar los valores de datos subyacentes del modelo de PowerPivot. Podría tener que modificar las expresiones para convertir los datos en el tipo de datos correcto, o agregar o quitar una función de agregado. Por ejemplo, para convertir el tipo de datos de cadena en entero, utilice `=CInt`. Compruebe siempre que el informe muestra los valores esperados de los datos del modelo de PowerPivot antes de publicar el informe.  
  
 Se generan vistas previas de las imágenes de un informe en una Galería de PowerPivot solo si se cumplen las siguientes condiciones:  
  
-   El informe y el libro PowerPivot que proporciona los datos deben estar almacenados juntos en la misma Galería de PowerPivot.  
  
-   El informe solo contiene datos PowerPivot de un origen de datos PowerPivot.  
  
## <a name="see-also"></a>Consulte también  
 [Interfaz de usuario del Diseñador de consultas MDX de Analysis Services &#40;Generador de informes&#41;](../analysis-services-mdx-query-designer-user-interface-report-builder.md)   
 [Expresiones &#40;Generador de informes y SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
