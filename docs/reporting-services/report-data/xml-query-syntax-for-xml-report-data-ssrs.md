---
title: Sintaxis de consulta XML para los datos de informe XML | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- namespaces [Reporting Services]
- data processing extensions [Reporting Services], data sources
- xmldp [Reporting Services]
- XML [Reporting Services], data retrieval
ms.assetid: d203886f-faa1-4a02-88f5-dd4c217181ef
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: dd1bccb6bff8f19e9abb779310033f4685b31f67
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "77081346"
---
# <a name="xml-query-syntax-for-xml-report-data-ssrs"></a>Sintaxis de consulta XML para los datos de informe XML (SSRS)
  En [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], se pueden crear conjuntos de datos para orígenes de datos XML. Después de definir un origen de datos, se crea una consulta para el conjunto de datos. En función del tipo de datos XML a los que señala el origen de datos, la consulta del conjunto de datos se crea incluyendo un elemento XML **Query** o una ruta de acceso de elemento. Un elemento XML **Query** empieza con una etiqueta **\<Consulta>** e incluye espacios de nombres y elementos XML que varían en función del origen de datos. Una ruta de acceso de elemento es independiente del espacio de nombres y especifica qué nodos y atributos de nodo se utilizan de los datos XML subyacentes con una sintaxis del tipo de XPath. Para más información sobre las rutas de acceso de elemento, vea [Sintaxis de ruta de acceso de elemento para datos de informe XML &#40;SSRS&#41;](../../reporting-services/report-data/element-path-syntax-for-xml-report-data-ssrs.md).  
  
 Se pueden crear orígenes de datos XML para los siguientes tipos de datos XML:  
  
-   Documentos XML a los que señala una dirección URL mediante el protocolo HTTP  
  
-   Extremos de servicios web que devuelven datos XML  
  
-   Datos XML incrustados  
  
 La forma en que se especifica un elemento XML **Query** o una ruta de acceso de elemento depende del tipo de los datos XML.  
  
 En el caso de los documentos XML, el elemento XML **Query** es opcional. Si se incluye, puede contener un elemento XML **ElementPath**. El valor del elemento XML **ElementPath** utiliza la sintaxis de la ruta de acceso de elemento. Los elementos XML **Query** y **ElementPath** se incluyen para procesar los espacios de nombres correctamente cuando lo requieran los datos XML del origen de datos.  
  
 Para un extremo de servicios web al que señala una dirección URL de cadena de conexión, el elemento XML **Query** define el método del servicio web, la acción SOAP o ambos. El proveedor de datos XML crea una solicitud de servicio web que recupera los datos XML que se utilizarán para el informe.  
  
> [!NOTE]  
>  Cuando un espacio de nombres de servicio web incluye un carácter de barra diagonal ( **/)** , deben incluirse tanto el método del servicio web como la acción SOAP, de manera que la extensión de procesamiento de datos XML pueda derivar el espacio de nombres correctamente.  
  
 En el caso de los documentos XML incrustados, el elemento XML **Query** define los datos XML incrustados que se van a utilizar, incluye espacios de nombres opcionales y contiene un elemento XML **ElementPath**opcional.  
  
## <a name="specifying-query-parameters-for-xml-data"></a>Especificar parámetros de consulta para datos XML  
 Puede especificar parámetros de consulta para documentos XML.  
  
-   Para solicitudes de dirección URL, los parámetros de consulta se incluyen como parámetros de dirección URL estándar.  
  
-   Para solicitudes de servicio web, los parámetros de consulta se pasan al método del servicio web. Para definir un parámetro de consulta, utilice la página **Parámetros** del cuadro de diálogo **Propiedades del conjunto de datos** . 
  
### <a name="example"></a>Ejemplo  
 En los ejemplos de la tabla siguiente se muestra cómo se recuperan los datos desde el servicio web del servidor de informes, un documento XML y datos XML incrustados.  
  
|Origen de datos XML|Ejemplo de consulta|  
|---------------------|-------------------|  
|Datos XML del servicio web obtenidos a través del método <xref:ReportService2010.ReportingService2010.ListChildren%2A> .|`<Query>`<br /><br /> `<Method Name="ListChildren" Namespace="https://schemas.microsoft.com/sqlserver/2005/06/30/reporting/reportingservices" />`<br /><br /> `</Query>`|  
|Datos XML del servicio web obtenidos a través de SoapAction.|`<Query xmlns=namespace>`<br /><br /> `<SoapAction>https://schemas/microsoft.com/sqlserver/2005/03/23/reporting/reportingservices/ListChildren</SoapAction>`<br /><br /> `</Query>`|  
|Documento XML o datos XML incrustados que usan espacios de nombres.<br /><br /> Elemento de consulta que especifica los espacios de nombres de una ruta de acceso de elemento.|`<Query xmlns:es="https://schemas.microsoft.com/StandardSchemas/ExtendedSales">`<br /><br /> `<ElementPath>/Customers/Customer/Orders/Order/es:LineItems/es:LineItem</ElementPath>`<br /><br /> `</Query>`|  
|Documento XML incrustado.|`<Query>`<br /><br /> `<XmlData>`<br /><br /> `<Customers>`<br /><br /> `<Customer ID="1">Bobby</Customer>`<br /><br /> `</Customers>`<br /><br /> `</XmlData>`<br /><br /> `<ElementPath>Customer {@}</ElementPath>`<br /><br /> `</Query>`|  
|Documento XML que usa los valores predeterminados.|*No query*.<br /><br /> La ruta de acceso de elemento se deriva del propio documento XML y es independiente del espacio de nombres.|  
  
> [!NOTE]  
>  El primer ejemplo de servicio web muestra el contenido del servidor de informes que usa el método <xref:ReportService2006.ReportingService2006.ListChildren%2A> . Para ejecutar esta consulta, es necesario crear un nuevo origen de datos y establecer la cadena de conexión en `https://localhost/reportserver/reportservice2006.asmx`. El método <xref:ReportService2006.ReportingService2006.ListChildren%2A> toma dos parámetros: **Item** y **Recursive**. Establezca el valor predeterminado de **Item** en **/** y de **Recursive** en **1**.  
  
## <a name="specifying-namespaces"></a>Especificar espacios de nombres  
 Use el elemento XML **Query** para especificar los espacios de nombres que se usan en los datos XML del origen de datos. En la siguiente consulta XML se utiliza el espacio de nombres **sales**. Los nodos de elemento XML **ElementPath** para `sales:LineItems` y `sales:LineItem` usan el espacio de nombres **sales**.  
  
```  
<Query xmlns:sales=  
"https://schemas.microsoft.com/StandardSchemas/ExtendedSales">  
   <SoapAction>  
      https://schemas.microsoft.com/SalesWebService/ListOrders   
   </SoapAction>  
   <ElementPath>  
      Customers/Customer/Orders/Order/sales:LineItems/sales:LineItem  
   </ElementPath>  
</Query>  
```  
  
 Para especificar el espacio de nombres del proveedor de datos de manera que el espacio de nombres predeterminado permanezca vacío, utilice **xmldp**. Esto se muestra en el ejemplo siguiente.  
  
### <a name="example"></a>Ejemplo  
 En los ejemplos siguientes se utiliza el documento XML DPNamespace.xml, que se proporciona después de la tabla a modo de ilustración. En esta tabla se muestran dos ejemplos de sintaxis de ruta de acceso de elemento XML que incluye prefijos de espacios de nombres.  
  
|Elemento de consulta XML|Campos resultantes en el conjunto de datos|  
|-----------------------|-------------------------------------|  
|\<Query/>|Valor A: `https://schemas.microsoft.com/...`<br /><br /> Valor B: `https://schemas.microsoft.com/...`<br /><br /> Valor C: `https://schemas.microsoft.com/...`|  
|`<xmldp:Query xmlns:xmldp="https://schemas.microsoft.com/sqlserver/2005/02/reporting/XmlDPQuery" xmlns:ns="https://schemas.microsoft.com/...">`<br /><br /> `<xmldp:ElementPath>Root {}/ns:Element2/Node</xmldp:ElementPath>`<br /><br /> `</xmldp:Query>`|Valor D<br /><br /> Valor E<br /><br /> Valor F|  
  
#### <a name="xml-document-dpnamespacexml"></a>Documento XML: DPNamespace.xml  
 Puede copiar este documento XML y guardarlo en una dirección URL disponible para el Diseñador de informes con objeto de poder usarlo como origen de datos XML, por ejemplo, https://localhost/DPNamespace.xml.  
  
```  
<Root xmlns:ns="https://schemas.microsoft.com/...">  
   <ns:Element1>  
      <Node>Value A</Node>  
      <Node>Value B</Node>  
      <Node>Value C</Node>  
   </ns:Element1>  
   <ns:Element2>  
      <Node>Value D</Node>  
      <Node>Value E</Node>  
      <Node>Value F</Node>  
   </ns:Element2>  
</Root>  
```  
  
## <a name="see-also"></a>Consulte también  
 [Tipo de conexión XML &#40;SSRS&#41;](../../reporting-services/report-data/xml-connection-type-ssrs.md)   
 [Tutoriales de Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-tutorials-ssrs.md)  
  
  
