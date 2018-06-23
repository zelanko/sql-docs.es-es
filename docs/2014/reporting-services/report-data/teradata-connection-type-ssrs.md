---
title: Tipo de conexión de Teradata (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b02779c2-a6b9-453c-815f-adad53353952
caps.latest.revision: 8
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 021352dc9685cb1af5327b657ea6a7b6434664e4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104194"
---
# <a name="teradata-connection-type-ssrs"></a>Tipo de conexión de Teradata (SSRS)
  Para incluir en un informe datos de una base de datos relacional de Teradata, debe tener un conjunto de datos basado en un origen de datos de informe de tipo Teradata. Este tipo de origen de datos integrado está basado en la extensión de procesamiento de datos del proveedor administrado de .NET para Teradata.  
  
 Utilice la información de este tema para crear un origen de datos. Para obtener instrucciones detalladas, consulte [agregar y comprobar una conexión de datos o un origen de datos &#40;el generador de informes y SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Cadena de conexión  
 Póngase en contacto con el administrador de bases de datos y solicite la información de conexión y las credenciales que debe usar para conectar con el origen de datos. En el ejemplo de cadena de conexión siguiente se especifica una base de datos de Teradata en el servidor especificado con una dirección IP:  
  
```  
data source=<IP Address>  
```  
  
 Para más información sobre ejemplos de cadenas de conexión, vea [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](../data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
##  <a name="Credentials"></a> Credenciales  
 Se necesitan credenciales para ejecutar consultas y obtener una vista previa del informe localmente y desde el servidor de informes.  
  
 Después de publicar el informe, es posible que necesite cambiar las credenciales para el origen de datos de tal forma que, cuando el informe se ejecute en el servidor de informes, los permisos para recuperar los datos sean válidos.  
  
 Para obtener más información, consulte [las conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) o [especificar credenciales en el generador de informes](../specify-credentials-in-report-builder.md).  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
##  <a name="Remarks"></a> Comentarios  
 Para poder conectarse a un origen de datos de Teradata, el administrador del sistema debe haber instalado la versión del proveedor de datos de .NET para Teradata que admite la recuperación de datos de la base de datos de Teradata. Este proveedor de datos debe estar instalado en el mismo equipo que el Generador de informes, además de en el servidor de informes.  
  
 Este proveedor de datos no admite todos los modos de entrega de informes. No se admite la entrega de informes a través de suscripciones controladas por datos para esta extensión de procesamiento de datos. Para más información, vea [Usar un origen de datos externo para obtener información de los suscriptores &#40;suscripción controlada por datos&#41;](../subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md) en la documentación de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Libros en pantalla[ de ](http://go.microsoft.com/fwlink/?linkid=121312).  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
##  <a name="Models"></a> Modelos de informe  
 Para crear un conjunto de datos a partir de un modelo de informe que esté basado en un origen de datos de Teradata, el modelo debe estar diseñado en el Diseñador de modelos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] y ser publicado en un servidor de informes.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
##  <a name="Related"></a> Secciones relacionadas  
 Estas secciones de la documentación proporcionan información conceptual detallada sobre los datos de informe, así como información de procedimientos acerca de cómo definir, personalizar y usar las partes de un informe que están relacionadas con datos.  
  
 [Agregar datos a un informe &#40;el generador de informes SSRS&#41;](report-datasets-ssrs.md)  
 Proporciona información general sobre cómo obtener acceso a los datos del informe.  
  
 [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 Proporciona información sobre las conexiones de datos y los orígenes de datos.  
  
 [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Proporciona información sobre conjuntos de datos compartidos e incrustados.  
  
 [Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  
 Proporciona información sobre la colección de campos que genera la consulta del conjunto de datos.  
  
 [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) en la documentación relativa a [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] en los [Libros en pantalla](http://go.microsoft.com/fwlink/?linkid=121312) de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
 Proporciona información detallada sobre la compatibilidad de versiones y plataformas para cada extensión de datos.  
  
 [Usar Reporting Services de SQL Server 2008 con el proveedor de datos de .NET Framework para Teradata](http://go.microsoft.com/fwlink/?LinkID=130848)  
 Proporciona información detallada sobre cómo trabajar con esta extensión de datos.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
## <a name="see-also"></a>Vea también  
 [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expresiones &#40;Generador de informes y SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  