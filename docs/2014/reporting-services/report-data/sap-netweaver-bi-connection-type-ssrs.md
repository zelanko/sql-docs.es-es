---
title: Tipo de conexión de SAP NetWeaver BI (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f985856b-31d5-4e56-844b-8a8ee38da67e
caps.latest.revision: 9
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 8cd1548cb8fb22a49900cc916dc1fde610993a05
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198130"
---
# <a name="sap-netweaver-bi-connection-type-ssrs"></a>Tipo de conexión de SAP NetWeaver BI (SSRS)
  Para incluir en un informe datos de un origen de datos de SAP NetWeaver® Business Intelligence externo, debe tener un conjunto de datos basado en un origen de datos de informe de tipo [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)]. Este tipo de origen de datos integrado está basado en la extensión de datos del proveedor de datos [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 1.0 para [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)].  
  
 Esta extensión de datos permite recuperar datos multidimensionales de InfoCubes, MultiProviders (InfoCubes virtual) y consultas habilitadas para web definidas en un origen de datos [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] externo.  
  
 Utilice la información de este tema para crear un origen de datos. Para obtener instrucciones detalladas, consulte [agregar y comprobar una conexión de datos o un origen de datos &#40;el generador de informes y SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="support"></a> Versiones admitidas  
 El proveedor de datos se ha desarrollado para SAP BW 3.5 y 7.0 y se ha probado en estas soluciones.  
  
-   Paquete de soporte 20 para SAP BW 3.5 y 7.0  
  
 Para la autenticación integrada de Windows, el proveedor se ha desarrollado para los siguientes sistemas y se ha probado en ellos.  
  
-   Paquete de soporte 20 de SAP Portals 6.40  
  
-   Paquete de soporte de portales 7.0 11 de SAP  
  
-   SAP Duet 1.0  
  
##  <a name="Connection"></a> Cadena de conexión  
 Póngase en contacto con el administrador de la base de datos y solicite la información de conexión y las credenciales que debe usar para conectar con el origen de datos. En el siguiente ejemplo de cadena de conexión se especifica un origen de datos de [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] en un servidor que usa el puerto 8000 y XML para Analysis Services (XMLA) en Internet con el protocolo SOAP:  
  
```  
DataSource=http://mySAPNetWeaverBIServer:8000/sap/bw/xml/soap/xmla  
```  
  
 Para más información sobre ejemplos de cadenas de conexión, vea [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](../data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
  
  
##  <a name="Credentials"></a> Credenciales  
 Se necesitan credenciales para ejecutar consultas y obtener una vista previa del informe localmente y desde el servidor de informes.  
  
 Después de publicar el informe, es posible que necesite cambiar las credenciales para el origen de datos de tal forma que, cuando el informe se ejecute en el servidor de informes, los permisos para recuperar los datos sean válidos.  
  
 Para obtener más información, consulte [las conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) o [especificar credenciales en el generador de informes](../specify-credentials-in-report-builder.md).  
  
  
  
##  <a name="Query"></a> Consultas  
 Se puede utilizar el diseñador gráfico de consultas en modo de diseño o de consulta para crear consultas de expresiones multidimensionales (MDX) examinando las estructuras de datos subyacentes en el origen de datos. En tiempo de diseño, para ver los resultados, se pueden ejecutar consultas desde el diseñador de consultas de forma interactiva. La consulta creada define los campos del conjunto de datos. En tiempo de ejecución, se devuelven los datos reales desde el origen de datos. Utilice el diseñador gráfico de consultas para realizar las siguientes acciones:  
  
-   En modo de diseño, arrastrar dimensiones, miembros, propiedades de miembros y cifras clave desde el origen de datos hasta un panel de datos para crear una consulta MDX. Para definir más campos de conjunto de datos, se pueden arrastrar miembros calculados desde el panel Miembros calculados hasta el panel de datos.  
  
-   En modo de consulta, arrastrar dimensiones, miembros, propiedades de miembros y cifras clave hasta el panel de consulta, o escribir texto MDX directamente en el panel de consulta. Para definir más campos de conjunto de datos, se pueden arrastrar miembros calculados desde el panel Miembros calculados hasta el panel de datos.  
  
 Mientras se generan las consultas, el diseñador de consultas agrega automáticamente propiedades predeterminadas a la consulta MDX. Para incluir propiedades distintas de las predeterminadas, debe modificar manualmente la consulta MDX.  
  
 Para más información sobre el trabajo con este diseñador de consultas, vea [Interfaz de usuario del Diseñador de consultas SAP NetWeaver BI &#40;Generador de informes&#41;](../sap-netweaver-bi-query-designer-user-interface-report-builder.md).  
  
  
  
##  <a name="Extended"></a> Propiedades de campo extendidas  
 El origen de datos [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] admite propiedades de campo extendidas. Propiedades de campo extendidas son propiedades además `Value` y `IsMissing` que se definen para un campo de conjunto de datos mediante la extensión de procesamiento de datos. Las propiedades extendidas incluyen propiedades predefinidas y propiedades personalizadas. Las propiedades predefinidas son propiedades comunes para varios orígenes de datos. Las propiedades personalizadas son únicas para cada origen de datos.  
  
### <a name="working-with-field-properties"></a>Trabajar con propiedades de campo  
 Las propiedades de campo extendidas no aparecen en el panel Datos de informe como elementos que se puedan arrastrar al diseño del informe. En su lugar, arrastre el campo primario de la propiedad al informe y, a continuación, cambie la propiedad predeterminada de `Value` a la propiedad que desea utilizar. Por ejemplo, si se crease el nombre de campo **Calendar Year/Month Level 01** en un diseñador de consultas MDX colocando un nivel del panel Metadatos en el panel Consulta, se usaría la sintaxis siguiente para hacer referencia a la propiedad extendida personalizada **Nombre largo** en una expresión:  
  
 `=Fields!Calendar_Year_Month_Level_01("Long Name")`  
  
 El nombre de la propiedad de campo extendida aparecerá en la información sobre herramientas al mantener el mouse encima de un campo del panel Metadatos. Para obtener más información acerca de los diseñadores de consultas puede utilizar para explorar los datos subyacentes, vea [SAP NetWeaver BI Query Designer User Interface](sap-netweaver-bi-query-designer-user-interface.md).  
  
> [!NOTE]  
>  Solo existirán valores para las propiedades de campo extendidas si el origen de datos ofrece estos valores cuando el informe se ejecuta y recupera los datos de sus conjuntos de datos. A continuación, puede hacer referencia a esos `Field` valores de propiedad de cualquier expresión mediante la sintaxis descrita más adelante. No obstante, dado que estos campos son específicos de este proveedor de datos y no son parte del lenguaje RDL (Report Definition Language), los cambios que se realicen en estos valores no se guardarán con la definición de informe.  
  
 Para hacer referencia a propiedades extendidas predefinidas en una expresión, se utiliza la sintaxis siguiente:  
  
-   *Fields!nombreDeCampo.nombreDePropiedad*  
  
-   *Fields!nombreDeCampo("nombreDePropiedad")*  
  
 Para hacer referencia a propiedades extendidas personalizadas en una expresión, se utiliza la sintaxis siguiente:  
  
-   *Fields!nombreDeCampo("nombreDePropiedad")*  
  
  
  
### <a name="predefined-field-properties"></a>Propiedades de campo predefinidas  
 En la siguiente tabla se ofrece una lista de las propiedades de campo predefinidas que se pueden usar para un origen de datos [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] .  
  
|**Propiedad**|**Tipo**|**Descripción o valor esperado**|  
|------------------|--------------|---------------------------------------|  
|`Value`|`Object`|Especifica el valor de los datos del campo.|  
|`IsMissing`|`Boolean`|Indica si se ha encontrado el campo en el conjunto de datos resultante.|  
|`FormattedValue`|`String`|Devuelve un valor con formato para una cifra clave.|  
|`BackgroundColor`|`String`|Devuelve el color de fondo del campo, definido en la base de datos.|  
|`Color`|`String`|Devuelve el color de primer plano del elemento, definido en la base de datos.|  
|`Key`|`Object`|Devuelve la clave de un nivel.|  
|`LevelNumber`|`Integer`|En jerarquías de elementos primarios y secundarios, devuelve el número de nivel o dimensión.|  
|`ParentUniqueName`|`String`|En jerarquías de elementos primarios y secundarios, devuelve el nombre completo del nivel primario.|  
|`UniqueName`|`String`|Devuelve el nombre completo de un nivel. Por ejemplo, el `UniqueName` el valor de un empleado puede ser *[0D_Company]. [ 10D_Department]. [11]* .|  
  
 Para más información sobre el uso de campos y propiedades de campo en una expresión, vea [Colecciones integradas en expresiones &#40;Generador de informes y SSRS&#41;](../report-design/built-in-collections-in-expressions-report-builder.md).  
  
  
  
##  <a name="Remarks"></a> Comentarios  
 Este proveedor de datos no admite todos los modos de entrega de informes. No se admite la entrega de informes a través de suscripciones controladas por datos para esta extensión de procesamiento de datos. Para más información, vea [Usar un origen de datos externo para obtener información de los suscriptores &#40;suscripción controlada por datos&#41;](../subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md).  
  
 Para obtener más información, vea el tema sobre cómo [usar SQL Server 2008 Reporting Services con SAP NetWeaver Business Intelligence](http://go.microsoft.com/fwlink/?LinkId=167352).  
  
  
  
##  <a name="HowTo"></a> Temas de procedimientos  
 Esta sección contiene instrucciones paso a paso para trabajar con conexiones de datos, orígenes de datos y conjuntos de datos.  
  
 [Agregar y comprobar una conexión de datos o un origen de datos &#40;el generador de informes SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Crear un conjunto de datos compartido o un conjunto de datos incrustado &#40;Generador de informes y SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Agregar un filtro a un conjunto de datos &#40;Generador de informes y SSRS&#41;](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
  
##  <a name="Related"></a> Secciones relacionadas  
 Estas secciones de la documentación proporcionan información conceptual detallada sobre los datos de informe, así como información de procedimientos acerca de cómo definir, personalizar y usar las partes de un informe que están relacionadas con datos.  
  
 [Agregar datos a un informe &#40;el generador de informes SSRS&#41;](report-datasets-ssrs.md)  
 Proporciona información general sobre cómo obtener acceso a los datos del informe.  
  
 [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 Proporciona información sobre las conexiones de datos y los orígenes de datos.  
  
 [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Proporciona información sobre conjuntos de datos compartidos e incrustados.  
  
 [Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  
 Proporciona información sobre la colección de campos de conjunto de datos que genera la consulta.  
  
 [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md)  
 Proporciona información detallada sobre la compatibilidad de versiones y plataformas para cada extensión de datos.  
  
 
  
## <a name="see-also"></a>Vea también  
 [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expresiones &#40;Generador de informes y SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  