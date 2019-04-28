---
title: Controlar errores y advertencias (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- errors [XML for Analysis]
- inline errors [XMLA]
- SOAP faults [XML for Analysis]
- XML for Analysis, errors
- faults [XML for Analysis]
- messages [XML for Analysis]
- XMLA, errors
- warnings [XML for Analysis]
- inline warnings [XMLA]
ms.assetid: ab895282-098d-468e-9460-032598961f45
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 856886a5edfa5dcae604b44f5c2dca356ba0addb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62702134"
---
# <a name="handling-errors-and-warnings-xmla"></a>Controlar errores y advertencias (XMLA)
  Control de errores es necesario cuando un documento de XML for Analysis (XMLA) [Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) o [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) llamada al método no se ejecuta, se ejecuta correctamente, pero genera errores o advertencias, o se ejecuta correctamente pero devuelve resultados que contienen errores.  
  
|Error|Notificación|  
|-----------|---------------|  
|La llamada al método XMLA no se ejecuta|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Devuelve un mensaje de error SOAP que contiene los detalles del error.<br /><br /> Para obtener más información, vea la sección [controlar errores de SOAP](#handling_soap_faults).|  
|Errores o advertencias en una llamada a método correcta|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] incluye un [error](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/error-element-xmla) o [advertencia](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/warning-element-xmla) (elemento) para cada error o advertencia, respectivamente, en el [mensajes](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/messages-element-xmla) propiedad de la [raíz](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/root-element-xmla) elemento que contiene los resultados de la llamada al método.<br /><br /> Para obtener más información, vea la sección [controlar errores y advertencias](#handling_errors_and_warnings).|  
|Errores en el resultado de una llamada a método correcta|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] incluye un elemento incorporado `error` o `warning` (elemento) para el error o advertencia, respectivamente, en la correspondiente [celda](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) o [fila](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/row-element-xmla) elemento de los resultados de la llamada al método.<br /><br /> Para obtener más información, vea la sección [controlar errores y advertencias insertados](#handling_inline_errors_and_warnings).|  
  
##  <a name="handling_soap_faults"></a> Controlar errores de SOAP  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] devuelve un error de SOAP cuando se producen las siguientes situaciones:  
  
-   El mensaje SOAP que contiene el método XMLA no estaba bien formado o la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no lo pudo validar.  
  
-   Se ha producido un error de comunicaciones o de otro tipo que afecta al mensaje SOAP que contiene el método XMLA.  
  
-   El método XMLA no se ejecutó en la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Los códigos de error de SOAP para XMLstartA empiezan por "XMLForAnalysis", seguido de un punto y del código de resultado HRESULT hexadecimal. Por ejemplo, un código de error de "`0x80000005`" tiene el formato "`XMLForAnalysis.0x80000005`". Para obtener más información sobre el formato de error de SOAP, consulte la información sobre errores de SOAP en Simple Object Access Protocol (SOAP) 1.1 de W3C.  
  
### <a name="fault-code-information"></a>Información del código de error  
 En la tabla siguiente se muestra la información de código de error de XMLA incluida en la sección de detalles de la respuesta SOAP. Las columnas son los atributos de un error en la sección de detalles de un error de SOAP.  
  
|Nombre de columna|Tipo|Descripción|Permitida NULL<sup>1</sup>|  
|-----------------|----------|-----------------|------------------------------|  
|`ErrorCode`|`UnsignedInt`|Código de retorno que indica la ejecución correcta o el error del método. El valor hexadecimal debe convertirse en un valor `UnsignedInt`.|No|  
|`WarningCode`|`UnsignedInt`|Código de retorno que indica una condición de advertencia. El valor hexadecimal debe convertirse en un valor `UnsignedInt`.|Sí|  
|`Description`|`String`|Texto y descripción del error o la advertencia devueltos por el componente que generó el error.|Sí|  
|`Source`|`String`|Nombre del componente que generó el error o la advertencia.|Sí|  
|`HelpFile`|`String`|Ruta de acceso o dirección URL del tema o el archivo de Ayuda que describe el error o la advertencia.|Sí|  
  
 <sup>1</sup> indica si los datos, es necesarios y deben devolverse, o si los datos son opcionales y se permite una cadena nula si la columna no se aplica.  
  
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
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] devuelve la propiedad `Messages` en el elemento `root` de un comando si se producen las siguientes situaciones después de ejecutarse dicho comando:  
  
-   El método se ejecutó correctamente, pero se produjo un error en la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] después de la llamada a método correcta.  
  
-   La instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] devuelve una advertencia cuando el comando se ejecuta correctamente.  
  
 La propiedad `Messages` sigue al resto de las propiedades contenidas en el elemento `root` y puede contener uno o más elementos `Message`. A su vez, cada elemento `Message` puede contener un elemento `error` o `warning` único que describa cualquier error o advertencia, respectivamente, que se hayan producido para el comando especificado.  
  
 Para obtener más información sobre los errores y advertencias que se encuentran en el `Messages` propiedad, vea [elemento Messages &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/messages-element-xmla).  
  
### <a name="handling-errors-during-serialization"></a>Controlar errores durante la serialización  
 Si se produce un error después de la [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia ha comenzado a serializar la salida de un comando ejecutado correctamente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] devuelve un [excepción](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/exception-element-xmla) elemento en otro espacio de nombres en el momento del error. A continuación, la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cierra todos los elementos abiertos para que el documento XML que se envía al cliente sea válido. La instancia también devuelve un elemento `Messages` que contiene la descripción del error.  
  
##  <a name="handling_inline_errors_and_warnings"></a> Controlar errores y advertencias insertados  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] devuelve un elemento `error` o `warning` insertado para un comando si el método XMLA en sí se ejecutó correctamente, pero se produjo un error específico de un elemento de datos en los resultados devueltos por el método en la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] después de haberse realizado correctamente la llamada al método XMLA.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Proporciona inline `error` y `warning` elementos si problemas específicos de una celda o a otros datos que están dentro de un `root` elemento mediante el [MDDataSet](https://docs.microsoft.com/bi-reference/xmla/xml-data-types/mddataset-data-type-xmla) se producen el tipo de datos, como la seguridad de un error o dar formato a Error en una celda. En estos casos, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] devuelve un elemento `error` o `warning` en el elemento `Cell` o `row` que contiene el error o la advertencia, respectivamente.  
  
 El ejemplo siguiente muestra un conjunto de resultados que contiene un error en el conjunto de filas devuelto por una `Execute` método mediante el [instrucción](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) comando.  
  
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
 [Desarrollo con XMLA en Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
