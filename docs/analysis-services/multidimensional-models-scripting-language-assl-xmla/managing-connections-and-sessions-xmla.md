---
title: Administrar conexiones y sesiones (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- statefulness [XML for Analysis]
- statelessness [XML for Analysis]
- XML for Analysis, sessions
- states [XML for Analysis]
- XMLA, sessions
- sessions [XML for Analysis]
ms.assetid: b83bb3ff-09be-4fda-9d1d-6248e04ffb21
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 52392cf2a1af25e0f67634286e371fb2bef408f3
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="managing-connections-and-sessions-xmla"></a>Administrar conexiones y sesiones (XMLA)
  *Disponibilidad de estados* es una condición durante el cual el servidor conserva la identidad y el contexto de un cliente entre las llamadas de método. *Dinamismo* es una condición durante el cual el servidor no recuerda la identidad y el contexto de un cliente al finalizar una llamada al método.  
  
 Para proporcionar disponibilidad de Estados, XML for Analysis (XMLA) admite *sesiones* que permiten una serie de instrucciones que se va a realizarse conjuntamente. Un ejemplo de este tipo de serie de instrucciones sería la creación de un miembro calculado que se vaya a utilizar en consultas posteriores.  
  
 En general, en XMLA las sesiones se ajustan al comportamiento siguiente descrito por la especificación de OLE DB 2.6:  
  
-   Las sesiones definen el ámbito de contexto de comandos y transacciones.  
  
-   Se pueden ejecutar varios comandos en el contexto de una sesión única.  
  
-   Compatibilidad con transacciones en el contexto XMLA es a través de los comandos específicos del proveedor enviados con el [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md) método.  
  
 XMLA define una manera de admitir sesiones en un entorno web de modo similar al enfoque utilizado por el protocolo de creación y control de versiones distribuidas (DAV) para implementar el bloqueo en un entorno de acoplamiento flexible. Esta implementación se asemeja a DAV en que se permite al proveedor finalizar sesiones por distintas razones (por ejemplo, se supera un tiempo de espera o se produce un error de conexión). Cuando se admiten sesiones, los servicios web deben tenerlo en cuenta y estar listos para controlar conjuntos de comandos interrumpidos que se deben reiniciar.  
  
 La especificación de protocolo simple de acceso a objetos (SOAP) de World Wide Web Consortium (W3C) recomienda utilizar encabezados SOAP para generar nuevos protocolos sobre mensajes SOAP. En la tabla siguiente se enumeran los atributos y los elementos de encabezado SOAP que XMLA define para iniciar, mantener y cerrar una sesión.  
  
|Encabezado SOAP|Description|  
|-----------------|-----------------|  
|BeginSession|Este encabezado solicita al proveedor que cree una nueva sesión. El proveedor deber responder mediante la construcción de una nueva sesión y la devolución de su identificador de sesión como parte del encabezado Session en la respuesta SOAP.|  
|SessionId|El área para valor contiene el identificador de sesión que se debe utilizar en cada llamada a método para el resto de la sesión. El proveedor de la respuesta SOAP envía esta etiqueta y el cliente también debe enviar este atributo con cada elemento de encabezado Session.|  
|Session|Debe utilizarse este encabezado en cada una de las llamadas a método que tiene lugar en la sesión; además, el identificador de sesión debe incluirse en el área para valor del encabezado.|  
|EndSession|Para finalizar la sesión, utilice este encabezado. El identificador de sesión debe incluirse en el área para valor.|  
  
> [!NOTE]  
>  Un identificador de sesión no garantiza que una sesión sea válida. Si la sesión expira (por ejemplo, se agota el tiempo de espera o se pierde la conexión), el proveedor puede optar por finalizar y revertir las acciones de esa sesión. Como resultado, todas las llamadas a método realizadas posteriormente desde el cliente con el identificador de sesión generan un error que señala una sesión no válida. El cliente debe controlar esta condición y estar preparado para reenviar las llamadas a método de la sesión desde el principio.  
  
## <a name="legacy-code-example"></a>Ejemplo de código heredado  
 En el ejemplo siguiente se muestra cómo se admiten las sesiones.  
  
1.  Para comenzar la sesión, agregue un encabezado BeginSession en SOAP a la llamada al método XMLA saliente desde el cliente. El área para valor aparece inicialmente en blanco porque todavía no se conoce el identificador de sesión.  
  
    ```  
    <SOAP-ENV:Envelope  
       xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/"  
       SOAP-ENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">  
       <SOAP-ENV:Header>  
          <XA:BeginSession  
             xmlns:XA="urn:schemas-microsoft-com:xml-analysis"  
             xsi:type="xsd:int"  
             mustUnderstand="1"/>  
       </SOAP-ENV:Header>  
       <SOAP-ENV:Body>  
          ...<!-- Discover or Execute call goes here.-->  
       </SOAP-ENV:Body>  
    </SOAP-ENV:Envelope>  
    ```  
  
2.  El mensaje de respuesta SOAP del proveedor incluye el identificador de sesión en el área de encabezado devuelto, el uso de la etiqueta de encabezado XMLA \<SessionId >.  
  
    ```  
    <SOAP-ENV:Header>  
       <XA:Session  
          xmlns:XA="urn:schemas-microsoft-com:xml-analysis"  
          SessionId="581"/>  
    </SOAP-ENV:Header>  
    ```  
  
3.  El encabezado Session debe agregarse para cada llamada a método de la sesión, con el identificador de sesión devuelto por el proveedor.  
  
    ```  
    <SOAP-ENV:Header>  
       <XA:Session  
          xmlns:XA="urn:schemas-microsoft-com:xml-analysis"  
          mustUnderstand="1"  
          SessionId="581"/>  
    </SOAP-ENV:Header>  
    ```  
  
4.  Cuando la sesión ha terminado, la \<EndSession > etiqueta se utiliza, que contiene el valor de Id. de sesión relacionado.  
  
    ```  
    <SOAP-ENV:Header>  
       <XA:EndSession  
          xmlns:XA="urn:schemas-microsoft-com:xml-analysis"  
          xsi:type="xsd:int"  
          mustUnderstand="1"  
          SessionId="581"/>  
    </SOAP-ENV:Header>  
    ```  
  
## <a name="see-also"></a>Vea también  
 [Desarrollo con XMLA en Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
