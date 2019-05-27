---
title: Report Definition Language (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Reporting Services, RDL
- Reporting Services, RDL
- RDL [Reporting Services], about Report Definition Language
- SSRS, RDL
- Report Definition Language, about Report Definition Language
- Report Definition Language
- RDL [Reporting Services]
- reports [Reporting Services], definitions
ms.assetid: b18b025e-f4bd-4744-8f86-0ac9fb967548
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6480a8cefee9b71149c61bf952896a739526cf55
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66102497"
---
# <a name="report-definition-language-ssrs"></a>Report Definition Language (SSRS)
  El lenguaje RDL (Report Definition Language) es una representación XML de una definición de informe de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Una definición de informe contiene información acerca de la recuperación y el diseño de los datos de un informe. RDL está formado por elementos XML que cumplen la sintaxis XML creada para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Puede agregar sus propias funciones personalizadas para controlar los valores de elemento de informe, los estilos y el formato si obtiene acceso a los ensamblados de código en los archivos de definición de informe.  
  
 RDL promueve la interoperabilidad de productos de generación de informes comerciales al definir un esquema común que habilita el intercambio de definiciones de informe. Cualquier protocolo o interfaz de programación que funciona con XML se puede utilizar con RDL. RDL es:  
  
-   Un esquema XML para las definiciones de informe.  
  
-   Un formato de intercambio para las empresas y otros fabricantes.  
  
-   Un esquema extensible y abierto que admite espacios de nombres adicionales y elementos personalizados.  
  
##  <a name="bkmk_RDL_Specifications"></a> Especificaciones de RDL  
 Para descargar las especificaciones de versiones específicas de esquema, vea [Especificación del lenguaje RDL](https://go.microsoft.com/fwlink/?linkid=116865).  
  
##  <a name="bkmk_RDL_XML_Schema_Definition"></a> Definición de esquema XML de RDL  
 A [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se valida con un archivo de definición de esquema XML (XSD). El esquema define las reglas para dónde se pueden producir elementos RDL en un archivo .rdl. Un elemento incluye su tipo de datos y cardinalidad, es decir, el número de repeticiones que se permiten. Los elementos pueden ser simples o complejos. Un elemento simple no tiene elementos o atributos secundarios. Un elemento complejo tiene elementos secundarios y opcionalmente, atributos.  
  
 Por ejemplo, el esquema incluye el elemento RDL `ReportParameters` que es del tipo complejo `ReportParametersType`. Por convención, un tipo complejo para un elemento es el nombre del elemento seguido de la palabra `Type`. Un elemento `ReportParameters` puede estar contenido en el elemento `Report` (un tipo complejo) y puede contener elementos `ReportParameter`. Un `ReportParameterType` es un tipo simple que solo puede tener uno de los siguientes valores: `Boolean`, `DateTime`, `Integer`, `Float` o `String`. Para obtener más información sobre los tipos de datos de esquema XML, vea [XML Schema Part 2: Datatypes Second Edition](https://go.microsoft.com/fwlink/?linkid=4871) (Parte 2 del esquema XML: tipos de datos, segunda edición).  
  
 El XSD de RDL está disponible en el archivo ReportDefinition.xsd, que se encuentra en la carpeta Extras del CD-ROM del producto. También está disponible en el servidor de informes a través de la siguiente dirección URL: http://servername/reportserver/reportdefinition.xsd.  
  
##  <a name="bkmk_Creating_RDL"></a> Crear RDL  
 Debido a la naturaleza abierta y extensible de RDL, se pueden compilar diversas herramientas y aplicaciones que generan RDL basándose en su esquema XML.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona varias herramientas para crear archivos RDL. Para obtener más información, vea [Herramientas de Reporting Services](../tools/reporting-services-tools.md).  
  
 Una de las maneras más fáciles de generar RDL desde una aplicación es usar las clases [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] del espacio de nombres <xref:System.Xml> y del espacio de nombres <xref:System.Linq> . Una clase en particular, la clase **XmlTextWriter** , se puede utilizar para escribir RDL. Con **XmlTextWriter**, puede generar una definición de informe completa en cualquier aplicación [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] . Los programadores también pueden ampliar RDL agregando elementos de informe personalizados con propiedades personalizadas. Para más información sobre la clase **XmlTextWriter** y el espacio de nombres <xref:System.Xml> , vea la Guía del programador de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] . Para obtener más información sobre Language-Integrated Query (LINQ), busque "LINQ to XML" en MSDN.  
  
 La extensión de archivo estándar para los archivos de definición de informe es .rdl. También puede desarrollar archivos de definición de informe de cliente, que tienen extensiones .rdlc. El tipo MIME para ambas extensiones es text/xml. Para más información sobre los informes, vea [Informes de Reporting Services &#40;SSRS&#41;](reporting-services-reports-ssrs.md).  
  
##  <a name="bkmk_RDL_Types"></a> Tipos de RDL  
 En la tabla siguiente se enumeran los tipos usados en los atributos y elementos del lenguaje RDL.  
  
|Tipo|Descripción|  
|----------|-----------------|  
|`Binary`|Una propiedad con un valor binario codificado de base 64.|  
|`Boolean`|Propiedad con `true` o `false` como valor del objeto. A menos que se especifique lo contrario, el valor de un objeto booleano opcional omitido es `False`.|  
|`Date`|Propiedad con un valor de fecha o fecha y hora especificado por completo con el formato de fecha ISO8601: YYYY-MM-DD[THH:MM[:SS[.S]]].|  
|`Enum`|Propiedad con un valor de texto de cadena que debe estar en una lista de valores designados.|  
|`Float`|Propiedad con un valor de tipo Float. Se utiliza un punto (.) como separador decimal opcional.|  
|`Integer`|Propiedad con un valor de tipo Integer (int32).|  
|`Language`|Propiedad con un valor de texto que contiene un código de idioma y referencia cultural, como "es-es" para español de España. El valor debe ser un idioma específico o un idioma neutro para el que se defina un idioma predeterminado en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].|  
|`Name`|Propiedad con un valor de texto de cadena. Los nombres deben ser únicos en el espacio de nombres del elemento. Si no se especifica, el espacio de nombres de un elemento es el objeto contenedor más interno que tiene un nombre.|  
|`NormalizedString`|Una propiedad con un valor de texto de cadena que se ha normalizado.|  
|`Size`|Un elemento de tamaño debe contener un número (con un punto como un separador decimal opcional). Un designador debe seguir al número para una unidad de longitud de CSS como cm, mm, pulgadas, pt o pc. Dejar un espacio entre el número y el designador es opcional. Para obtener más información sobre los designadores de tamaño, vea la [Referencia de unidades de longitud de CSS](https://www.w3schools.com/CSSref/css_units.asp).<br /><br /> En RDL, el valor máximo para `Size` es de 160 pulgadas. El tamaño mínimo es de 0 pulgadas.|  
|`String`|Propiedad con un valor de texto de cadena.|  
|`UnsignedInt`|Una propiedad con un valor de tipo Integer (uint32) sin signo.|  
|`Variant`|Una propiedad con cualquier tipo XML sencillo.|  
  
##  <a name="bkmk_RDL_Data_Types"></a> Tipos de datos de RDL  
 La enumeración DataType define el tipo de datos de un atributo, una expresión o un parámetro en el lenguaje RDL. En la tabla siguiente se muestra cómo se corresponden los tipos de datos CLR (Common Language Runtime) con los tipos de datos RDL.  
  
|**Tipos CLR**|**Tipo de datos correspondiente**|  
|-----------------------|---------------------------------|  
|Boolean|Boolean|  
|DateTime, DateTimeOffset|DateTime|  
|Int16, Int32, UInt16, Byte, SByte|Integer|  
|Single, Double|float|  
|String, Char, GUID, Timespan|String|  
  
## <a name="see-also"></a>Vea también  
 [Buscar la versión del esquema de definición de informe &#40;SSRS&#41;](find-the-report-definition-schema-version-ssrs.md)   
 [Usar ensamblados personalizados con informes](../custom-assemblies/using-custom-assemblies-with-reports.md)   
 [Elementos de informe personalizados](../custom-report-items/custom-report-items.md)  
  
  
