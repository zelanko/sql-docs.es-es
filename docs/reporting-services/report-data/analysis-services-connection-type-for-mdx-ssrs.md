---
title: Tipo de conexión de Analysis Services para MDX (SSRS) | Microsoft Docs
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: bd2e7148-3124-4e07-9734-22333127c3be
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c108b2eaaf8aa0182b8192ab2d7868db84d531a6
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892486"
---
# <a name="analysis-services-connection-type-for-mdx-ssrs"></a>Tipo de conexión de Analysis Services para MDX (SSRS)
  Para incluir en el informe datos de un cubo de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , debe tener un conjunto de datos basado en un origen de datos de informe de tipo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Este tipo de origen de datos integrado está basado en la extensión de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Puede recuperar metadatos sobre dimensiones, jerarquías, niveles, indicadores clave de rendimiento (KPI), medidas y atributos desde un cubo de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para usarlos como datos de informe.  
  
 Esta extensión de procesamiento de datos admite parámetros de varios valores, agregados de servidor y credenciales administrados con independencia de la cadena de conexión.  
  
 Utilice la información de este tema para crear un origen de datos. Para obtener instrucciones paso a paso, vea [Agregar y comprobar una conexión de datos o un origen de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Cadena de conexión  
 Al conectarse a un cubo de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , se conecta al objeto de base de datos de una instancia de Analysis Services en un servidor. La base de datos podría tener varios cubos. El cubo se especifica en el diseñador de consultas al crear la consulta. En el siguiente ejemplo se muestra una cadena de conexión:  
  
```  
data source=<server name>;initial catalog=<database name>  
```  
  
 Para más información sobre ejemplos de cadenas de conexión, vea [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
  
##  <a name="Credentials"></a> Credenciales  
 Se necesitan credenciales para ejecutar consultas y obtener una vista previa del informe localmente y desde el servidor de informes.  
  
 Después de publicar el informe, es posible que necesite cambiar las credenciales para el origen de datos de tal forma que, cuando el informe se ejecute en el servidor de informes, los permisos para recuperar los datos sean válidos.  
  
 Desde un cliente de creación de informes, están disponibles las siguientes opciones para especificar las credenciales:  
  
-   Usuario actual de Windows (lo que se conoce también como seguridad integrada).  
  
-   Utilizar un nombre de usuario y una contraseña almacenados.  
  
-   Pedir las credenciales al usuario. Esta opción solo admite la seguridad integrada de Windows.  
  
-   No se necesitan credenciales. Para usar esta opción, debe tener la cuenta de ejecución desatendida configurada en el servidor de informes. Para más información, vea [Configurar la cuenta de ejecución desatendida &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) en la [documentación de Reporting Services](https://go.microsoft.com/fwlink/?linkid=121312) en msdn.microsoft.com.  
  
 Para obtener más información, vea [conexiones de datos, orígenes de datos y &#40;cadenas de conexión&#41; generador de informes y SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) o [especificar información de credenciales y conexión para los orígenes de datos de informe](specify-credential-and-connection-information-for-report-data-sources.md).  
  
  
##  <a name="Query"></a> Consultas  
 Después de establecer una conexión de datos a un origen de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , debe crear un conjunto de datos y definir una consulta de expresión multidimensional (MDX) que especifique los datos del cubo que se van a recuperar. Puede utilizar la exploración del diseñador gráfico de consultas MDX y seleccionar entre las estructuras de datos subyacentes en el origen de datos.  
  
 Puede especificar una consulta de varias maneras:  
  
-   Generar una consulta interactivamente. El Diseñador de consultas MDX de Analysis Services admite las siguientes vistas:  
  
    -   **Vista de diseño** : para crear una consulta MDX, se pueden arrastrar dimensiones, miembros, propiedades de miembros, medidas y KPI desde el explorador de metadatos hasta el panel **Datos** . Para definir más campos de conjunto de datos, se pueden arrastrar miembros calculados desde el panel Miembros calculados hasta el panel de datos.  
  
    -   **Vista de consulta** : para crear una consulta MDX, se pueden arrastrar dimensiones, miembros, propiedades de miembros, medidas y KPI desde el explorador de metadatos hasta el panel Consulta. El texto MDX se puede editar directamente en el panel de consulta. Para definir más campos de conjunto de datos, se pueden arrastrar miembros calculados desde el panel Miembros calculados hasta el panel de consulta.  
  
     Para más información, vea [Interfaz de usuario del Diseñador de consultas MDX de Analysis Services &#40;Generador de informes&#41;](https://msdn.microsoft.com/library/7e288eee-2d37-485e-a6a0-dbba5e041e26).  
  
-   Importar una consulta MDX existente desde un informe. Utilice el botón **Importar consulta** para ir a un archivo .rdl e importar una consulta. Puede importar una consulta desde un informe que contenga un conjunto de datos incrustado que se base en un origen de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . No se admite la importación directa de una consulta MDX desde un archivo .mdx.  
  
 Durante el diseño, ejecute la consulta para ver un conjunto de resultados. Los resultados de la consulta se recuperan automáticamente como un conjunto de filas planas. Las columnas del conjunto de resultados de una consulta rellenan la colección de campos de un conjunto de datos. Después de crear la consulta, vea la colección de campos del conjunto de datos generada a partir de los metadatos en el panel Datos de informe. Cuando el informe se ejecuta, los datos reales se devuelven desde el origen de datos externo.  
  
 La extensión de procesamiento de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite propiedades de campo de conjunto de datos extendidas. Éstos son valores disponibles del origen de datos externo, pero no aparecen en el panel Datos de informe. En el informe se pueden usar las propiedades de campo extendidas admitidas por la extensión de procesamiento de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] con la colección integrada **Fields** . Para las propiedades que tengan valores en el origen de datos, se puede tener acceso a valores de propiedad predefinidos como **FormattedValue**, **Color**o **UniqueName**. Para obtener más información, vea [Propiedades de campo extendidas para una base de datos de Analysis Services &#40;SSRS&#41;](../../reporting-services/report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md).  
  
  
##  <a name="Parameters"></a> Parámetros  
 Para incluir parámetros de consulta, cree un filtro en el área de filtro del diseñador de consultas y marque el filtro como un parámetro. Para cada filtro, se crea automáticamente un conjunto de datos para proporcionar los valores disponibles. De forma predeterminada, estos conjuntos de datos no aparecen en el panel Datos de informe. Para más información, vea [Definir parámetros en el diseñador de consultas MDX para Analysis Services &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/define-parameters-in-the-mdx-query-designer-for-analysis-services.md) y [Mostrar conjuntos de datos ocultos para los valores de parámetro de datos multidimensionales &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/show-hidden-datasets-for-parameter-values-multidimensional-data.md).  
  
 De forma predeterminada, cada parámetro de informe tiene el tipo de datos **Text**. Una vez creados los parámetros de informe, podría suceder que tenga que cambiar los valores predeterminados. Para más información, vea [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
  
##  <a name="Remarks"></a> Comentarios  
 La extensión de datos de Analysis Services está basada en el protocolo XMLA (XML for Analysis). Los conjuntos de resultados de los cubos se recuperan mediante el protocolo XMLA como un conjunto de filas sin información de estructura jerárquica. No se admiten jerarquías desiguales. Para más información, vea [Jerarquías desiguales](https://docs.microsoft.com/analysis-services/multidimensional-models/user-defined-hierarchies-ragged-hierarchies).  
  
 También puede recuperar datos de un cubo de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] del tipo de origen de datos OLE DB. Para obtener más información, vea [Tipo de conexión OLE DB &#40;SSRS&#41;](../../reporting-services/report-data/ole-db-connection-type-ssrs.md).  
  
 Para más información sobre la compatibilidad de versiones, vea [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) en la documentación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en los [Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]](https://go.microsoft.com/fwlink/?linkid=121312).  
  
  
##  <a name="Related"></a> Secciones relacionadas  
 Estas secciones de la documentación proporcionan información conceptual detallada sobre los datos de informe, así como información de procedimientos acerca de cómo definir, personalizar y usar las partes de un informe que están relacionadas con datos.  
  
 [Conjuntos de datos de informe &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 Proporciona información general sobre cómo obtener acceso a los datos del informe.  
  
 [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
 Proporciona información sobre las conexiones de datos y los orígenes de datos.  
  
 [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Proporciona información sobre conjuntos de datos compartidos e incrustados.  
  
 [Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 Proporciona información sobre la colección de campos de conjunto de datos que genera la consulta.  
  
 [Propiedades de campo extendidas para una base de datos de Analysis Services &#40;SSRS&#41;](../../reporting-services/report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md)  
 Proporciona información sobre los campos adicionales disponibles a través del proveedor de datos XMLA.  
  
 [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) en la documentación relativa a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en los [Libros en pantalla](https://go.microsoft.com/fwlink/?linkid=121312) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 Proporciona información detallada sobre la compatibilidad de versiones y plataformas para cada extensión de datos.  
  
  
## <a name="see-also"></a>Consulte también  
 [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
