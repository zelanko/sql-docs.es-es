---
title: Administrar conjuntos de datos compartidos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 2cbb1fa3-959e-4df6-9887-ebc93cc1b686
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c498917b7f4f293d1721d09e68d1ba40672c1dc2
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66107210"
---
# <a name="manage-shared-datasets"></a>Administrar conjuntos de datos compartidos
  En [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], los conjuntos de datos compartidos recuperan los datos de los orígenes de datos compartidos que se conectan a los orígenes de datos externos. Un conjunto de datos compartido proporciona una manera de compartir una consulta para ayudar a proporcionar un conjunto coherente de datos para varios informes. La consulta del conjunto de datos puede incluir parámetros de conjunto de datos. Puede configurar un conjunto de datos compartido para almacenar en memoria caché los resultados de la consulta para combinaciones de parámetros concretas al usarse por primera vez o especificando una programación. Puede utilizar el almacenamiento en caché del conjunto de datos compartido en combinación con el almacenamiento en caché de los informes y las fuentes de datos de informe para ayudar a administrar el acceso a un origen de datos.  
  
 Los conjuntos de datos compartidos solo utilizan orígenes de datos compartidos, no orígenes de datos incrustados. Un conjunto de datos compartido puede estar basado en cualquier origen de datos para una extensión de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] admitida o un modelo de informe.  
  
## <a name="creating-and-using-shared-datasets"></a>Crear y utilizar conjuntos de datos compartidos  
 Para crear un conjunto de datos compartido, debe utilizar una aplicación que cree un archivo de definición de conjunto de datos compartido (.rsd). Para ello, puede utilizar una de las siguientes aplicaciones:  
  
-   Generador de informes. Use el modo de diseño de conjunto de datos compartidos y guarde el conjunto de datos compartido en un servidor de informes o sitio de SharePoint.  
  
-   Diseñador de informes de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] . Cree conjuntos de datos compartidos en la carpeta Conjunto de datos compartidos en el Explorador de soluciones. Para publicar un conjunto de datos compartido, impleméntelo en un servidor de informes o sitio de SharePoint.  
  
-   Cargar un archivo de definición de conjuntos de datos compartidos (.rsd): puede cargar un archivo al servidor de informes o sitio de SharePoint. En un sitio de SharePoint. Un archivo cargado no se valida con el esquema hasta que el conjunto de datos compartido esté almacenado en memoria caché o se use en un informe.  
  
 La definición del conjunto de datos compartidos incluye una consulta, parámetros de conjunto de datos que incluyen valores predeterminados, opciones de datos con distinción entre mayúsculas y minúsculas, y filtros de conjunto de datos. Los valores que establezca en la definición se usarán siempre que el conjunto de datos compartido se incluya en un informe.  
  
 Para utilizar un conjunto de datos compartido en un informe, abra una aplicación como el Generador de informes, busque el servidor de informes o el sitio de SharePoint y seleccione el conjunto de datos compartido. De este modo, agrega una instancia del conjunto de datos compartido al informe. En el informe, no puede ver ni cambiar la consulta o el origen de datos compartido para el conjunto de datos compartido. Puede especificar un conjunto adicional de valores de propiedad del conjunto de datos que se apliquen a la instancia en el informe. Por ejemplo, puede agregar un filtro o cambiar opciones de datos como la distinción entre mayúsculas y minúsculas. Para más información, vea [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md) en la [documentación del Generador de informes](https://go.microsoft.com/fwlink/?LinkId=154494) en msdn.microsoft.com.  
  
## <a name="managing-shared-datasets"></a>Administrar los conjuntos de datos compartidos  
 Para administrar las propiedades de un conjunto de datos compartidos publicado, puede usar el Administrador de informes para un servidor de informes en modo nativo o las páginas de aplicación de un sitio de SharePoint, si implementó el servidor de informes en el modo integrado de SharePoint. Las tareas que puede realizar en un conjunto de datos compartido dependen de sus asignaciones de roles y de los permisos del nivel de sitio y de elemento, incluidos los permisos de la carpeta, si la herencia de permisos está en vigor. La seguridad en el nivel de elemento de los conjuntos de datos compartidos sigue el mismo modelo que la de los informes. Para más información, vea [Proteger los elementos de un conjunto de datos compartido](../security/secure-shared-dataset-items.md).  
  
 Puede administrar las propiedades de elementos de conjuntos de datos compartidas, incluido el origen de datos compartido que se utilizará, independientemente del informe que use el conjunto de datos compartido o el origen de datos compartido del que dependa. Para cambiar la consulta u otras propiedades de conjunto de datos que forman parte de la definición del conjunto de datos compartido, debe modificar la definición.  
  
### <a name="manage-shared-dataset-item-properties"></a>Administrar las propiedades de elemento del conjunto de datos compartido  
 En la siguiente tabla se enumeran las propiedades de elemento que puede cambiar para un elemento de conjunto de datos compartido.  
  
|||  
|-|-|  
|Editar nombre|Cambie el nombre del conjunto de datos compartido. Todas las referencias en los elementos dependientes continuarán funcionando.|  
|Editar descripción|Cambie la descripción del conjunto de datos compartido.|  
|Modificar el tiempo de espera de ejecución de la consulta|Establezca el tiempo de espera de ejecución de la consulta en segundos. Cero (0) segundos significa que no hay tiempo de espera. Determina el número de segundos antes de que la consulta de conjunto de datos supere el tiempo de espera. Para no especificar ningún valor de tiempo de espera, utilice 0. Para más información, vea [Establecer valores de tiempo de espera para el procesamiento de informes y conjuntos de datos compartidos &#40;SSRS&#41;](../report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md).|  
|Ver elementos dependientes|Vea los elementos que utilizan este conjunto de datos compartido: los elementos de informe publicados, los orígenes de datos compartidos y los informes.|  
  
 Se configuran automáticamente la siguientes propiedades de conjunto de datos compartidas adicionales:  
  
|Property|Descripción|  
|--------------|-----------------|  
|HasDataSourceCredentials|Si el origen de datos compartido asociado tiene las credenciales guardadas en el servidor de informes.|  
|HasUserProfileDependencies|Si el informe tiene una referencia a la colección Usuario global en su consulta o en expresiones de filtro.|  
  
## <a name="viewing-or-changing-the-shared-dataset-definition"></a>Ver o cambiar la definición del conjunto de datos compartido  
 Las propiedades del conjunto de datos compartido, incluidos la consulta, los parámetros de conjunto de datos, los valores predeterminados, los filtros del conjunto de datos y las opciones de datos como la intercalación y la distinción entre mayúsculas y minúsculas, se guardan en su definición. Si tiene los permisos necesarios, puede ver y cambiar la definición.  
  
 Para ver o cambiar la definición del conjunto de datos compartido, modifique el conjunto de datos compartido en una aplicación como el Generador de informes en modo de diseño del conjunto de datos compartido. Después de realizar los cambios, guarde la definición del conjunto de datos compartido en el servidor o sitio.  
  
 Otra manera de ver la definición del conjunto de datos compartido en XML es utilizar la sintaxis de acceso de direcciones URL en el Administrador de informes. Por ejemplo, para ver los valores predeterminados para cada parámetro de conjunto de datos, puede utilizar el siguiente comando de acceso de dirección URL para mostrar una definición del conjunto de datos compartido denominada DataSet1 en el servidor de informes:  
  
```  
http://localhost/reportserver/?/DataSet1&rs:command=GetShareddatasetDefinition  
```  
  
## <a name="controlling-access-to-the-shared-dataset-definition"></a>Controlar el acceso a la definición del conjunto de datos compartido  
 De forma predeterminada, las siguientes tareas se aplican a las operaciones en conjuntos de datos compartidos.  
  
-   **Ver informes** . Permite ver elementos de conjunto de datos compartidos y propiedades de elementos.  
  
-   **Usar informes** . Permite leer las definiciones de conjuntos de datos.  
  
-   **Administrar informes** . Permite crear y eliminar los conjuntos de datos compartidos y modificar sus propiedades.  
  
-   **Establecer la seguridad de elementos individuales** . Permite ver y modificar la configuración de seguridad de los conjuntos de datos compartidos.  
  
 Para más información sobre qué tareas y permisos controlan el acceso a las propiedades del origen de datos en un servidor de informes en modo nativo, vea [Proteger los elementos de un conjunto de datos compartido](../security/secure-shared-dataset-items.md).  
  
 El administrador del sitio determina los permisos para ver y modificar las propiedades de los elementos de una biblioteca de SharePoint. Para más información, vea [Referencia de permisos de sitio y lista de SharePoint para los elementos del servidor de informes](../security/sharepoint-site-and-list-permission-reference-for-report-server-items.md).  
  
## <a name="how-to-work-with-shared-dataset-properties-on-a-report-server"></a>Trabajar con las propiedades del conjunto de datos compartido en un servidor de informes  
 Puede utilizar diversas herramientas para trabajar con conjuntos de datos compartidos. En la tabla siguiente se resumen los enfoques y las herramientas, y se proporciona un vínculo a instrucciones adicionales.  
  
|Tarea|Herramienta|Vínculo|  
|----------|----------|----------|  
|Agregue un conjunto de datos compartido o cambie las propiedades de definición del conjunto de datos compartido.|Guardar en el Generador de informes.<br /><br /> Implementar en el Diseñador de informes.<br /><br /> Cargar un archivo .rsd en el Administrador de informes.|[Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md) en la [documentación del Generador de informes](https://go.microsoft.com/fwlink/?LinkId=154494) en msdn.microsoft.com<br /><br /> [Cargar archivo &#40;página del Administrador de informes&#41;](../upload-file-page-report-manager.md)<br /><br /> Si carga un conjunto de datos compartido antes de que se publique el origen de datos compartido del que depende, debe enlazar manualmente el conjunto de datos compartido al origen de datos compartido. Para más información, vea [Página de propiedades generales, conjuntos de datos compartidos &#40;Administrador de informes&#41;](../general-properties-page-shared-datasets-report-manager.md).|  
|Cambiar las propiedades de elemento del conjunto de datos compartido.|Administrador de informes|[Página de propiedades generales, conjuntos de datos compartidos &#40;Administrador de informes&#41;](../general-properties-page-shared-datasets-report-manager.md)|  
|Especificar propiedades de conjunto de datos compartido adicionales para una instancia del conjunto de datos compartido en un informe.|Diseñador de informes del Generador de informes|[Propiedades del conjunto de datos (cuadro de diálogo), Consulta](../dataset-properties-dialog-box-query.md)|  
|Enlazar a un origen de datos compartido diferente para un conjunto de datos compartido.|Administrador de informes|[Selección de origen de datos &#40;página del Administrador de informes&#41;](../data-source-selection-page-report-manager.md)|  
|Comprobar los valores predeterminados para los parámetros de conjunto de datos.|Abrir en el Generador de informes o usar la sintaxis de acceso de URL.|Por ejemplo:<br /><br /> `http://localhost/reportserver/?/DataSet1&rs:command=GetShareddatasetDefinition`|  
|Habilitar el almacenamiento en caché|Administrador de informes|[Almacenar en caché conjuntos de datos compartidos &#40;SSRS&#41;](../report-server/cache-shared-datasets-ssrs.md)<br /><br /> [Página de almacenamiento en caché, conjuntos de datos compartidos &#40;Administrador de informes&#41;](../caching-page-shared-datasets-report-manager.md)|  
|Crear o modificar un plan de actualización de la memoria caché|Administrador de informes|[Opciones de actualización de memoria caché &#40;Administrador de informes&#41;](../cache-refresh-options-report-manager.md)|  
|Ver el esquema de la definición del conjunto de datos compartido.|Administrador de informes|`http://<reportserver>/shareddatasetdefinition.xsd`|  
|En modo integrado de SharePoint, sincronizar la definición del conjunto de datos compartido entre el servidor de informes y el sitio de SharePoint|Páginas de aplicación de SharePoint|Cambiar las propiedades de elemento del conjunto de datos compartido<br /><br /> Cambiar las opciones de memoria caché<br /><br /> Cambiar el origen de datos compartido|  
  
## <a name="comparing-shared-datasets-with-other-report-server-items"></a>Comparar los conjuntos de datos compartidos con otros elementos del servidor de informes  
 Al administrar varios tipos de elementos en un servidor de informes, se hace más fácil entender la similitud de los elementos y la diferencia de otros elementos del servidor de informes.  
  
 Los conjuntos de datos compartidos son similares a los orígenes de datos compartidos e informes de las siguientes maneras:  
  
-   Al igual que los orígenes de datos compartidos, los conjuntos de datos compartidos se administran con independencia de los informes en los que se usan. Una parte de la administración de un conjunto de datos compartidos en un servidor de informes es la capacidad de cambiar el origen de datos compartidos del que depende sin necesidad de modificar su definición.  
  
-   Al igual que los informes, los conjuntos de datos compartidos pueden estar almacenados en memoria caché. Las credenciales que requiere el origen de datos deben cumplir las restricciones de almacenamiento en caché y se deben especificar valores predeterminados para cada parámetro. Para más información, vea [Almacenar en caché conjuntos de datos compartidos &#40;SSRS&#41;](../report-server/cache-shared-datasets-ssrs.md).  
  
-   Al igual que los informes, cada vez que se produce el procesamiento, se utiliza la definición actual del elemento en el servidor de informes. Si realiza cambios en un conjunto de datos compartido, cada informe que lo utilice empleará la definición actual en el servidor de informes cuando el informe se procese. Si el almacenamiento en memoria caché se habilita para el conjunto de datos compartido y se realizan cambios en la definición del conjunto de datos compartido, los cambios no se utilizan hasta que los datos de la memoria caché expiran. Puede utilizar planes de actualización de la memoria caché como ayuda para proporcionar un conjunto coherente de datos para varios informes.  
  
 Los conjuntos de datos compartidos se diferencian de los distintos elementos de informe publicados de la siguiente manera:  
  
-   A diferencia de lo que ocurre con los elementos de informe publicados, los cambios en la definición de un conjunto de datos compartido en un servidor de informes no desencadenan notificaciones de actualización cuando el informe se abre en un cliente de creación de informes. Al ejecutar el informe, se utilizan los datos de la definición del conjunto de datos compartido actual en el servidor de informes.  
  
 Los conjuntos de datos compartidos son similares a las suscripciones de las siguientes maneras:  
  
-   Pueden utilizar programaciones compartidas específicas de un elemento para el almacenamiento en memoria caché.  
  
-   Siguen las mismas reglas para especificar los valores de parámetros que las suscripciones.  
  
## <a name="see-also"></a>Vea también  
 [Administración de contenido del servidor de informes &#40;Modo nativo de SSRS&#41;](../report-server/report-server-content-management-ssrs-native-mode.md)   
 [Conceder permisos en un servidor de informes en modo nativo](../security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
