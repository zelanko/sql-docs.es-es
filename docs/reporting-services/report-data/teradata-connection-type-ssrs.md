---
title: "Tipo de conexión de Teradata (SSRS) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b02779c2-a6b9-453c-815f-adad53353952
caps.latest.revision: 10
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: c74e24e12f97d264780e712a1e7e5f3fbea6f9fb
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="teradata-connection-type-ssrs"></a>Tipo de conexión de Teradata (SSRS)
  Para incluir en un informe datos de una base de datos relacional de Teradata, debe tener un conjunto de datos basado en un origen de datos de informe de tipo Teradata. Este tipo de origen de datos integrado está basado en la extensión de procesamiento de datos del proveedor administrado de .NET para Teradata.  
  
 Utilice la información de este tema para crear un origen de datos. Para obtener instrucciones paso a paso, vea [Agregar y comprobar una conexión de datos o un origen de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Cadena de conexión  
 Póngase en contacto con el administrador de bases de datos y solicite la información de conexión y las credenciales que debe usar para conectar con el origen de datos. En el ejemplo de cadena de conexión siguiente se especifica una base de datos de Teradata en el servidor especificado con una dirección IP:  
  
```  
data source=<IP Address>  
```  
  
 Para más información sobre ejemplos de cadenas de conexión, vea [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34).  
  
##  <a name="Credentials"></a> Credenciales  
 Se necesitan credenciales para ejecutar consultas y obtener una vista previa del informe localmente y desde el servidor de informes.  
  
 Después de publicar el informe, es posible que necesite cambiar las credenciales para el origen de datos de tal forma que, cuando el informe se ejecute en el servidor de informes, los permisos para recuperar los datos sean válidos.  
  
 Para más información, vea [Conexiones de datos, orígenes de datos y cadenas de conexión &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) o [Especificar credenciales en el Generador de informes](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53).  
  
  
##  <a name="Remarks"></a> Comentarios  
 Para poder conectarse a un origen de datos de Teradata, el administrador del sistema debe haber instalado la versión del proveedor de datos de .NET para Teradata que admite la recuperación de datos de la base de datos de Teradata. Este proveedor de datos debe estar instalado en el mismo equipo que el Generador de informes, además de en el servidor de informes.  
  
 Este proveedor de datos no admite todos los modos de entrega de informes. No se admite la entrega de informes a través de suscripciones controladas por datos para esta extensión de procesamiento de datos. Para más información, vea [Usar un origen de datos externo para obtener información de los suscriptores &#40;suscripción controlada por datos&#41;](../../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md) en la documentación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Libros en pantalla[ de ](http://go.microsoft.com/fwlink/?linkid=121312).  
  
  
##  <a name="Models"></a> Modelos de informe  
 Para crear un conjunto de datos a partir de un modelo de informe que esté basado en un origen de datos de Teradata, el modelo debe estar diseñado en el Diseñador de modelos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] y ser publicado en un servidor de informes.  
  
  
##  <a name="Related"></a> Secciones relacionadas  
 Estas secciones de la documentación proporcionan información conceptual detallada sobre los datos de informe, así como información de procedimientos acerca de cómo definir, personalizar y usar las partes de un informe que están relacionadas con datos.  
  
 [Conjuntos de datos de informe &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 Proporciona información general sobre cómo obtener acceso a los datos del informe.  
  
 [Conexiones de datos, orígenes de datos y cadenas de conexión en el generador de informes](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)  
 Proporciona información sobre las conexiones de datos y los orígenes de datos.  
  
 [Informe incrusta los conjuntos de datos y conjuntos de datos compartidos &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Proporciona información sobre conjuntos de datos compartidos e incrustados.  
  
 [Colección de campos de conjunto de datos &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 Proporciona información sobre la colección de campos que genera la consulta del conjunto de datos.  
  
 [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) en la documentación relativa a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en los [Libros en pantalla](http://go.microsoft.com/fwlink/?linkid=121312) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 Proporciona información detallada sobre la compatibilidad de versiones y plataformas para cada extensión de datos.  
  
 [Usar Reporting Services de SQL Server 2008 con el proveedor de datos de .NET Framework para Teradata](http://go.microsoft.com/fwlink/?LinkID=130848)  
 Proporciona información detallada sobre cómo trabajar con esta extensión de datos.  
  
  
## <a name="see-also"></a>Vea también  
 [Parámetros de informe &#40; El generador de informes y el Diseñador de informes &#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtro, grupo y ordenar los datos &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expresiones &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  

