---
title: Datos de informe
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: sql-server-2014
ms.technology: reporting-services
ms.prod_service: reporting-services-native, reporting-services-sharepoint
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: be36e61a44a416283e77638f01005f1b3e16883b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67413053"
---
# <a name="report-data-in-sql-server-reporting-services-ssrs"></a>Datos de informe en SQL Server Reporting Services (SSRS)

  Los datos del informe pueden proceder de varios orígenes de datos de la organización. El primer paso para diseñar un informe es crear orígenes de datos y conjuntos de datos que representan los datos de informes subyacentes. Cada origen de datos incluye información de conexión de datos. Cada conjunto de datos incluye un comando de consulta que define el conjunto de campos que se van a usar como datos de un origen de datos. Para ver los datos de cada conjunto de datos, agregue una región de datos, como una tabla, una matriz, un gráfico o un mapa. Cuando se procesa el informe, las consultas se ejecutan en el origen de datos y cada región de datos se expande según sea necesario para mostrar los resultados de la consulta para el conjunto de datos.  
  
##  <a name="BkMk_ReportDataTerms"></a> Términos

 Si no está familiarizado con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] los conceptos, revise los siguientes términos [en Reporting Services conceptos &#40;SSRS&#41;](../reporting-services-concepts-ssrs.md): *conexión de datos*, orígenes de datos *incrustados*, *orígenes de datos compartidos*, conjuntos de datos *incrustados*, conjuntos de datos *compartidos*, *consultas de conjunto*de datos, elementos de *Informe*y *alertas de datos*.  
  
##  <a name="BkMk_ReportDataTips"></a>Sugerencias para especificar datos de informe

 Use la siguiente información para diseñar una estrategia de datos de informe.  
  
- **Orígenes de datos** Los orígenes de datos se pueden publicar y administrar independientemente de los informes de un servidor de informes o un sitio de SharePoint. Para cada origen de datos, usted o el propietario de la base de datos pueden administrar la información de conexión en un solo lugar. Las credenciales del origen de datos se almacenan de forma segura en el servidor de informes; no incluya contraseñas en la cadena de conexión. Puede redirigir el origen de datos de un servidor de prueba a un servidor de producción. Puede deshabilitar un origen de datos para suspender todos los informes que lo usan. Para obtener una lista de orígenes de datos admitidos, vea [conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
- **Conjuntos de valores** Los conjuntos de datos se pueden publicar y administrar independientemente de los informes o los orígenes de datos compartidos de los que dependen. Usted o el propietario de la base de datos pueden proporcionar consultas optimizadas para los autores de informes que se van a usar. Cuando cambie la consulta, todos los informes que usan el conjunto de datos compartido utilizan la consulta actualizada. Puede habilitar el almacenamiento en caché del conjunto de datos para mejorar el rendimiento. Puede programar el almacenamiento en caché de la consulta para un momento concreto o usar una programación compartida.  
  
- **Datos usados por los elementos de informe** Los elementos de informe pueden incluir los datos de los que dependen. Para más información sobre los elementos de informe, vea [Elementos de informe en el Diseñador de informes &#40;SSRS&#41;](../report-design/report-parts-in-report-designer-ssrs.md).  
  
- **Filtrar datos** Los datos del informe se pueden filtrar en la consulta o en el informe. Puede usar conjuntos de datos y variables de consulta para crear parámetros en cascada y proporcionar al usuario la posibilidad de reducir las opciones de miles de selecciones a un número más fácil de administrar. Puede filtrar los datos en una tabla o un gráfico basándose en los valores de parámetro u otros valores que especifique.  
  
- **Parámetros** de Los comandos de consulta de conjunto de DataSet que incluyen variables de consulta crean automáticamente parámetros de informe coincidentes. También puede crear los parámetros de forma manual. Al ver un informe, la barra de herramientas de informe muestra los parámetros. Los usuarios pueden seleccionar valores para controlar el aspecto del informe o de los datos del informe. Para personalizar los datos de destinatarios específicos, puede crear conjuntos de parámetros de informe con diferentes valores predeterminados vinculados a la misma definición de informe o usar el campo integrado `UserID`. Para más información, vea [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../report-design/report-parameters-report-builder-and-report-designer.md) y [Colecciones integradas en expresiones &#40;Generador de informes y SSRS&#41;](../report-design/built-in-collections-in-expressions-report-builder.md).  
  
- **Alertas de datos** Una vez publicado un informe, puede crear alertas basadas en los datos del informe y recibir mensajes de correo electrónico cuando cumpla las reglas especificadas.  
  
- **Agrupar y agregar datos** Los datos del informe se pueden agrupar y agregar en la consulta o en el informe. Si agrega valores a la consulta, puede continuar combinando valores en el informe dentro de los límites de lo que es significativo.  Para más información, vea [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md) y [Funciones del generador de informes - función de agregado](../report-design/report-builder-functions-aggregate-function.md).  
  
- **Ordenar datos** Los datos de informe se pueden ordenar en la consulta o en el informe. En las tablas, también puede agregar un botón de ordenación interactivo para permitir al usuario controlar el criterio de ordenación.  
  
- **Datos basados en expresiones** Dado que la mayoría de las propiedades del informe pueden estar basadas en expresiones y las expresiones pueden incluir referencias a campos de conjunto de datos y parámetros de informe, puede escribir expresiones eficaces para controlar los datos y el aspecto de los informes. Puede proporcionar a un usuario la capacidad de controlar los datos que visualiza si define parámetros.  
  
- **Mostrar datos de un conjunto de datos** Los datos de un conjunto de datos se muestran normalmente en una o varias regiones de datos, por ejemplo, una tabla y un gráfico.  
  
- **Mostrar datos de varios conjuntos de datos**  Puede escribir expresiones en una región de datos basada en un conjunto de datos que buscan valores o agregados en otros conjuntos de datos. Puede incluir subinformes en una tabla basada en un conjunto de datos para mostrar los datos de un origen de datos.  
  
## <a name="data-connections-data-sources-and-datasets"></a>Conexiones de datos, orígenes de datos y conjuntos de datos

 Use la lista siguiente como ayuda para definir orígenes de datos para un informe.  
  
- Considere si debe usar orígenes de datos y conjuntos de datos incrustados o compartidos. Colabore con los propietarios de los orígenes de datos para implementar y usar la tecnología de autenticación y autorización que sea adecuada para su organización.  
  
- Comprenda la arquitectura de nivel de datos de software de su organización y los problemas potenciales que surgen de los tipos de datos. Conozca cómo las extensiones de datos y de procesamiento de datos pueden afectar a los resultados de la consulta. Los tipos de datos difieren entre el origen de datos, los proveedores de datos y los tipos de datos almacenados en el archivo de definición de informe (.rdl).  
  
- Comprenda las herramientas y las arquitecturas de cliente y servidor de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Por ejemplo, en el Diseñador de informes, los informes se crean en un equipo cliente que usa tipos de orígenes de datos integrados. Cuando se publica un informe, los tipos de origen de datos deben ser compatibles con el servidor de informes o el sitio de SharePoint.  Para más información, vea [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md).  
  
- Los orígenes de datos y conjuntos de datos se crean en un informe y se publican en un servidor de informes o en un sitio de SharePoint desde una herramienta de creación de cliente. Los orígenes de datos se pueden crear directamente en el servidor de informes. Una vez que se publican, puede configurar las credenciales y otras propiedades en el servidor de informes. Para obtener más información, vea [conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) y [Reporting Services herramientas](../tools/reporting-services-tools.md).  
  
- Los orígenes de datos que puede usar dependen de las extensiones de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instaladas. La compatibilidad con los orígenes de datos puede diferir en lo relativo a herramienta de creación de cliente, versión del servidor de informes y plataforma del servidor de informes. Para más información, vea [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md).  
  
- Las credenciales del origen de datos varían según el tipo de origen de datos y de si los informes se muestran en el cliente, en el servidor de informes o en el sitio de SharePoint. Para más información, vea [Establecer permisos para elementos del servidor de informes en un sitio de SharePoint &#40;Reporting Services en el modo integrado de SharePoint&#41;](../security/set-permissions-for-report-server-items-on-a-sharepoint-site.md), [Especificar información de credenciales y conexión para los orígenes de datos de informes](../../integration-services/connection-manager/data-sources.md) e información de credenciales específica de cada herramienta en [Herramientas de Reporting Services](../tools/reporting-services-tools.md).  
  
## <a name="related-tasks"></a>Related Tasks

 Las tareas relacionadas con crear conexiones de datos, agregar datos de orígenes externos, conjuntos de datos y consultas.  
  
|||  
|-|-|  
|**Tareas comunes**|**Vínculos**|  
|Crear conexiones de datos|[Data Connections, Data Sources, and Connection Strings in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)|  
|Crear conjuntos de datos y consultas|[Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)|  
|Administrar orígenes de datos después de que se publican|[Administrar orígenes de datos de informe](manage-report-data-sources.md)|  
|Administrar conjuntos de datos compartidos cuando se publican|[Administración de conjuntos de datos compartidos](manage-shared-datasets.md)|  
|Crear y administrar alertas de datos|[Alertas de datos de Reporting Services](../tutorial-creating-a-basic-table-report-report-builder.md)|  
|Almacenar en caché un conjunto de datos compartido|[Almacenar en caché conjuntos de datos compartidos &#40;SSRS&#41;](../report-server/cache-shared-datasets-ssrs.md)|  
|Programar un conjunto de datos compartido para cargar previamente la memoria caché|[Programaciones](../subscriptions/schedules.md)|  
|Agregar una extensión de datos|[Implementar una extensión de procesamiento de datos](../extensions/data-processing/implementing-a-data-processing-extension.md)|