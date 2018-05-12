---
title: Controlar errores y advertencias (XMLA) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f2ba225f749364101f800efc4316b941bf18aac5
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="handling-errors-and-warnings-xmla"></a>Controlar errores y advertencias (XMLA)
  Control de errores es necesario cuando un documento de XML for Analysis (XMLA) [Discover](../../analysis-services/xmla/xml-elements-methods-discover.md) o [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md) llamada al método no se ejecuta, se ejecuta correctamente, pero genera errores o advertencias, o se ejecuta correctamente pero devuelve resultados que contienen errores.  
  
|Error|Notificación|  
|-----------|---------------|  
|La llamada al método XMLA no se ejecuta|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Devuelve un mensaje de error SOAP que contiene los detalles del error.<br /><br /> Para obtener más información, vea la sección [controlar errores de SOAP](#handling_soap_faults).|  
|Errores o advertencias en una llamada a método correcta|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] incluye un [error](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md) o [advertencia](../../analysis-services/xmla/xml-elements-properties/warning-element-xmla.md) (elemento) para cada error o advertencia, respectivamente, en la [mensajes](../../analysis-services/xmla/xml-elements-properties/messages-element-xmla.md) propiedad de la [raíz](../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) elemento que contiene los resultados de la llamada al método.<br /><br /> Para obtener más información, vea la sección [Handling Errors and Warnings](#handling_errors_and_warnings).|  
|Errores en el resultado de una llamada a método correcta|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] incluye un insertado **error** o **advertencia** , elemento de error o advertencia, respectivamente, con la correspondiente [celda](../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md) o [fila](../../analysis-services/xmla/xml-elements-properties/row-element-xmla.md) elemento de los resultados de la llamada al método.<br /><br /> Para obtener más información, vea la sección [control de errores y advertencias insertados](#handling_inline_errors_and_warnings).|  
  
##  <a name="handling_soap_faults"></a> Controlar errores de SOAP  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] devuelve un error de SOAP cuando se producen las siguientes situaciones:  
  
-   El mensaje SOAP que contiene el método XMLA no estaba bien formado o la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no lo pudo validar.  
  
-   Se ha producido un error de comunicaciones o de otro tipo que afecta al mensaje SOAP que contiene el método XMLA.  
  
-   El método XMLA no se ejecutó en la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Los códigos de error de SOAP para XMLstartA empiezan por "XMLForAnalysis", seguido de un punto y del código de resultado HRESULT hexadecimal. Por ejemplo, un código de error de "`0x80000005`" tiene el formato "`XMLForAnalysis.0x80000005`". Para obtener más información sobre el formato de error de SOAP, consulte la información sobre errores de SOAP en Simple Object Access Protocol (SOAP) 1.1 de W3C.  
  
### <a name="fault-code-information"></a>Información del código de error  
 En la tabla siguiente se muestra la información de código de error de XMLA incluida en la sección de detalles de la respuesta SOAP. Las columnas son los atributos de un error en la sección de detalles de un error de SOAP.  
  
|Nombre de columna|Tipo|Description|Permitida NULL<sup>1</sup>|  
|-----------------|----------|-----------------|------------------------------|  
|**ErrorCode**|**UnsignedInt**|Código de retorno que indica la ejecución correcta o el error del método. El valor hexadecimal debe convertirse en un **UnsignedInt** valor.|no|  
|**WarningCode**|**UnsignedInt**|Código de retorno que indica una condición de advertencia. El valor hexadecimal debe convertirse en un **UnsignedInt** valor.|Sí|  
|**Description**|**String**|Texto y descripción del error o la advertencia devueltos por el componente que generó el error.|Sí|  
|**Source**|**String**|Nombre del componente que generó el error o la advertencia.|Sí|  
|**HelpFile**|**String**|Ruta de acceso o dirección URL del tema o el archivo de Ayuda que describe el error o la advertencia.|Sí|  
  
 <sup>1</sup> indica si los datos son obligatorios y deben proporcionarse o si los datos son opcionales y se permite una cadena nula si la columna no se aplica.  
  
 A continuación se muestra un ejemplo de un error de SOAP que se produjo al no poderse realizar una llamada a método:  
  
```  
<?xml version="1.0"?>  
   <SOAP-ENV:Envelope  
   xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/"  
   SOAP-ENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">  
      <SOAP-ENV:Fault>  
         <faultcode>XMLAnalysisError.0x80000005</faultcode>  
         <faultstring>The XML for Analysis provider encountered an error.</faultstring>  
         <faultactor>XML for Analysis Provider</faultactor>  
         <detail>  
<Error  
ErrorCode="2147483653"  
Description="An unexpected error has occurred."  
Source="XML for Analysis Provider"  
HelpFile="" />  
         </detail>  
      </SOAP-ENV:Fault>  
</SOAP-ENV:Envelope>  
```  
  
##  <a name="handling_errors_and_warnings"></a> Controlar errores y advertencias  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Devuelve el **mensajes** propiedad en el **raíz** (elemento) para un comando si se producen las siguientes situaciones después de ejecuta este comando:  
  
-   El método se ejecutó correctamente, pero se produjo un error en la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] después de la llamada a método correcta.  
  
-   La instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] devuelve una advertencia cuando el comando se ejecuta correctamente.  
  
 El **mensajes** propiedad sigue todas las demás propiedades que están incluidas en el **raíz** elemento y puede contener uno o varios **mensaje** elementos. A su vez, cada uno de ellos **mensaje** elemento puede contener un único **error** o **advertencia** elemento que describe los errores o advertencias, respectivamente, que se produjeron en el comando especificado.  
  
 Para obtener más información sobre los errores y advertencias que se encuentran en el **mensajes** propiedad, vea [Messages, elemento &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-properties/messages-element-xmla.md).  
  
### <a name="handling-errors-during-serialization"></a>Controlar errores durante la serialización  
 Si se produce un error después de la [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia haya comenzado a serializar la salida de un comando ejecutado correctamente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] devuelve un [excepción](../../analysis-services/xmla/xml-elements-properties/exception-element-xmla.md) elemento en un espacio de nombres diferente en el momento del error. A continuación, la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cierra todos los elementos abiertos para que el documento XML que se envía al cliente sea válido. La instancia también devuelve una **mensajes** elemento que contiene la descripción del error.  
  
##  <a name="handling_inline_errors_and_warnings"></a> Control de errores y advertencias insertados  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Devuelve un insertado **error** o **advertencia** para un comando si no produjo error en el propio método XMLA, pero se produjo un error específico a un elemento de datos en los resultados devueltos por el método en el [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia después de que se ha realizado correctamente en la llamada al método XMLA.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proporciona **error** y **advertencia** elementos si problemas específicos de una celda o a otros datos que están dentro de un **raíz** elemento utilizando el [ MDDataSet](../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md) se producen tipo de datos, como un error de seguridad o un error de formato de una celda. En estos casos, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] devuelve un **error** o **advertencia** elemento en el **celda** o **fila** elemento que contiene el error o advertencia, respectivamente.  
  
 En el ejemplo siguiente se muestra un conjunto de resultados que contiene un error en el conjunto de filas devuelto por una **Execute** método mediante el [instrucción](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md) comando.  
  
```  
<return>  
   ...  
   <root>  
      ...  
      <CellData>  
      ...  
         <Cell CellOrdinal="10">  
            <Value>  
               <Error>  
                  <ErrorCode>2148497527</ErrorCode>   
                  <Description>Security Error.</Description>   
               </Error>  
            </Value>  
         </Cell>  
      </CellData>  
      ...  
   </root>  
   ...  
</return>  
```  
  
## <a name="see-also"></a>Vea también  
 [Desarrollar con XMLA en Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
