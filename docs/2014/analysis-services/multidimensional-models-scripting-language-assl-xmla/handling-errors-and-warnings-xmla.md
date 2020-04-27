---
title: Control de errores y advertencias (XMLA) | Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62702134"
---
# <a name="handling-errors-and-warnings-xmla"></a>Controlar errores y advertencias (XMLA)
  El control de errores es necesario cuando una llamada al método [Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) o [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) XML for Analysis (XMLA) no se ejecuta, se ejecuta correctamente, pero genera errores o advertencias, o se ejecuta correctamente, pero devuelve resultados que contienen errores.  
  
|Error|Generación de informes|  
|-----------|---------------|  
|La llamada al método XMLA no se ejecuta|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve un mensaje de error de SOAP que contiene los detalles del [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] error.<br /><br /> Para obtener más información, vea la sección [control de errores de SOAP](#handling_soap_faults).|  
|Errores o advertencias en una llamada a método correcta|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]incluye un elemento de [error](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/error-element-xmla) o [ADVERTENCIA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/warning-element-xmla) para cada error o advertencia, respectivamente, en la propiedad [messages](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/messages-element-xmla) del elemento [raíz](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/root-element-xmla) que contiene los resultados de la llamada al método.<br /><br /> Para obtener más información, vea la sección [control de errores y advertencias](#handling_errors_and_warnings).|  
|Errores en el resultado de una llamada a método correcta|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]incluye un elemento o `error` `warning` insertado para el error o advertencia, respectivamente, dentro del elemento de [celda](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) o [fila](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/row-element-xmla) adecuado de los resultados de la llamada al método.<br /><br /> Para obtener más información, vea la sección [control de errores y advertencias en línea](#handling_inline_errors_and_warnings).|  
  
##  <a name="handling-soap-faults"></a><a name="handling_soap_faults"></a>Control de errores de SOAP  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] devuelve un error de SOAP cuando se producen las siguientes situaciones:  
  
-   El mensaje SOAP que contiene el método XMLA no estaba bien formado o la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no lo pudo validar.  
  
-   Se ha producido un error de comunicaciones o de otro tipo que afecta al mensaje SOAP que contiene el método XMLA.  
  
-   El método XMLA no se ejecutó en la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Los códigos de error de SOAP para XMLstartA empiezan por "XMLForAnalysis", seguido de un punto y del código de resultado HRESULT hexadecimal. Por ejemplo, un código de error de "`0x80000005`" tiene el formato "`XMLForAnalysis.0x80000005`". Para obtener más información sobre el formato de error de SOAP, consulte la información sobre errores de SOAP en Simple Object Access Protocol (SOAP) 1.1 de W3C.  
  
### <a name="fault-code-information"></a>Información del código de error  
 En la tabla siguiente se muestra la información de código de error de XMLA incluida en la sección de detalles de la respuesta SOAP. Las columnas son los atributos de un error en la sección de detalles de un error de SOAP.  
  
|Nombre de la columna|Tipo|Descripción|Null permitido<sup>1</sup>|  
|-----------------|----------|-----------------|------------------------------|  
|`ErrorCode`|`UnsignedInt`|Código de retorno que indica la ejecución correcta o el error del método. El valor hexadecimal debe convertirse en un valor `UnsignedInt`.|No|  
|`WarningCode`|`UnsignedInt`|Código de retorno que indica una condición de advertencia. El valor hexadecimal debe convertirse en un valor `UnsignedInt`.|Sí|  
|`Description`|`String`|Texto y descripción del error o la advertencia devueltos por el componente que generó el error.|Sí|  
|`Source`|`String`|Nombre del componente que generó el error o la advertencia.|Sí|  
|`HelpFile`|`String`|Ruta de acceso o dirección URL del tema o el archivo de Ayuda que describe el error o la advertencia.|Sí|  
  
 <sup>1</sup> indica si los datos son obligatorios y deben devolverse, o si los datos son opcionales y se permite una cadena NULL si la columna no se aplica.  
  
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
  
##  <a name="handling-errors-and-warnings"></a><a name="handling_errors_and_warnings"></a>Control de errores y advertencias  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] devuelve la propiedad `Messages` en el elemento `root` de un comando si se producen las siguientes situaciones después de ejecutarse dicho comando:  
  
-   El método se ejecutó correctamente, pero se produjo un error en la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] después de la llamada a método correcta.  
  
-   La instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] devuelve una advertencia cuando el comando se ejecuta correctamente.  
  
 La propiedad `Messages` sigue al resto de las propiedades contenidas en el elemento `root` y puede contener uno o más elementos `Message`. A su vez, cada elemento `Message` puede contener un elemento `error` o `warning` único que describa cualquier error o advertencia, respectivamente, que se hayan producido para el comando especificado.  
  
 Para obtener más información sobre los errores y las advertencias que se `Messages` incluyen en la propiedad, vea [elemento messages &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/messages-element-xmla).  
  
### <a name="handling-errors-during-serialization"></a>Controlar errores durante la serialización  
 Si se produce un error después [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de que la instancia ya haya empezado a serializar la salida de un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] comando ejecutado correctamente, devuelve un elemento [Exception](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/exception-element-xmla) en un espacio de nombres diferente en el punto del error. A continuación, la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cierra todos los elementos abiertos para que el documento XML que se envía al cliente sea válido. La instancia también devuelve un elemento `Messages` que contiene la descripción del error.  
  
##  <a name="handling-inline-errors-and-warnings"></a><a name="handling_inline_errors_and_warnings"></a>Control de errores y advertencias en línea  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] devuelve un elemento `error` o `warning` insertado para un comando si el método XMLA en sí se ejecutó correctamente, pero se produjo un error específico de un elemento de datos en los resultados devueltos por el método en la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] después de haberse realizado correctamente la llamada al método XMLA.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]proporciona elementos y `error` `warning` insertados si se producen problemas específicos de una celda o de otros datos contenidos dentro de `root` un elemento mediante el tipo de datos [MDDataSet](https://docs.microsoft.com/bi-reference/xmla/xml-data-types/mddataset-data-type-xmla) , como un error de seguridad o un error de formato para una celda. En estos casos, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] devuelve un elemento `error` o `warning` en el elemento `Cell` o `row` que contiene el error o la advertencia, respectivamente.  
  
 En el ejemplo siguiente se muestra un conjunto de resultados que contiene un error en el conjunto de `Execute` filas devuelto desde un método mediante el comando [Statement](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) .  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Desarrollar con XMLA en Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
