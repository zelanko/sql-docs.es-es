---
title: Usar el Control RSClientPrint en aplicaciones personalizadas | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- RSPrintClient control
- print controls [Reporting Services]
- custom printing [Reporting Services]
- client-side printing
ms.assetid: 8c0bdd18-8905-4e22-9774-a240fc81a8a7
caps.latest.revision: 31
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 8afee187160da9d35efd0c7079b649bac7e73740
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="using-the-rsclientprint-control-in-custom-applications"></a>Usar el control RSClientPrint en aplicaciones personalizadas
  El [!INCLUDE[msCoName](../../../includes/msconame-md.md)] control ActiveX, **RSPrintClient**, proporciona la impresión del lado cliente para los informes que se ve en el Visor de HTML. Proporciona un **imprimir** cuadro de diálogo para que un usuario puede iniciar un trabajo de impresión, obtener una vista previa de un informe, especifique las páginas que desea imprimir y cambiar los márgenes. Durante una operación de impresión del lado cliente, el servidor de informes representa el informe en la extensión de representación en imágenes (EMF) y utiliza las capacidades de impresión del sistema operativo para crear el trabajo de impresión y enviarlo a una impresora.  
  
 La impresión del lado cliente ofrece un modo de controlar y mejorar la calidad de la copia impresa de un informe HTML anulando la configuración de impresión del explorador y utilizando, en su lugar, dimensiones de página, márgenes, texto de encabezados y pies de página del informe para crear la salida impresa. El control de impresión lee los valores de las propiedades del informe para establecer el tamaño de página y los márgenes.  
  
 Los desarrolladores que desean habilitar la característica de impresión del lado cliente en barras de herramientas de terceros o visores de tener acceso al control de ActiveX a través de la **RSClientPrint** objeto COM. El control se puede distribuir libremente. En la lista siguiente se ofrecen recomendaciones sobre el uso del control:  
  
-   Utilice el control para mejorar la impresión en informes basados en web. Puede especificar el objeto de cualquiera de los [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]-lenguajes de programación compatibles o en un script. El control no está diseñado para aplicaciones de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows Forms.  
  
-   Copie el archivo .cab de los archivos de programa  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] y agréguelo al código base de la aplicación personalizada.  
  
-   Use un \<objeto > etiquetas para especificar el control.  
  
-   Especifique una dirección URL relativa o completa al archivo .cab en el atributo OBJECT CODEBASE.  
  
-   Especifique la información de versión de su propia aplicación para el archivo .cab con el fin de realizar un seguimiento de la versión que se utiliza en su aplicación.  
  
-   Revise los temas de los Libros en pantalla que abordan la representación en imágenes (EMF) con el objetivo de conocer cómo se representan las páginas para la vista previa de impresión y la salida.  
  
## <a name="rsprintclient-overview"></a>Información general de RSPrintClient  
 El control muestra un cuadro de diálogo de impresión personalizado compatible con características comunes a otros cuadros de diálogo de impresión, incluida la vista previa de impresión, selecciones de páginas para especificar páginas e intervalos de páginas, márgenes y orientación. El control se empaqueta como un archivo CAB. El texto en el **impresión** cuadro de diálogo está traducido a todos los idiomas admitidos en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. **RSPrintClient** control ActiveX utiliza la extensión de representación de imágenes (EMF) para imprimir el informe. Se usa la siguiente información del dispositivo EMF: StartPage, EndPage, MarginBottom, MarginLeft, MarginTop, MarginRight, PageHeight y PageWidth. No se admite ninguna otra configuración de información de dispositivo para la representación en imágenes.  
  
### <a name="language-support"></a>Compatibilidad con idiomas  
 El control de impresión proporciona texto de la interfaz de usuario en distintos idiomas y acepta valores de entrada calibrados para diversos sistemas de medida. El sistema de idioma y la medición usa están determinados por la **referencia cultural** y **UICulture** propiedades. Ambas propiedades aceptan valores LCID. Si especifica un LCID para un idioma que es una variación de un idioma compatible, obtendrá el idioma que más se aproxime. Si especifica un LCID no compatible y para el que no existe ningún otro LCID que se aproxime, obtendrá Inglés (Estados Unidos).  
  
## <a name="using-rsclientprint-in-code"></a>Usar RSClientPrint en el código  
 El **RSClientPrint** objeto se usa para obtener acceso mediante programación para el control ActiveX y sus métodos y propiedades. El control proporciona un cuadro de diálogo modal para la vista previa de impresión.  
  
### <a name="specifying-default-values"></a>Especificar los valores predeterminados  
 Puede inicializar el **impresión** cuadro de diálogo con los valores de margen y página del informe. De forma predeterminada, el **impresión** cuadro de diálogo se inicializa con los valores de la definición de informe. Puede utilizar los valores predeterminados o especificar valores diferentes mediante el establecimiento de las propiedades en el objeto.  
  
 Todas las dimensiones están establecidas es milímetros. Conversión de medidas se produce en tiempo de ejecución si el **referencia cultural** y **UICulture** se establecen en las configuraciones regionales que no utilizan medidas métricas.  
  
 Para entender qué valores se utilizan para las dimensiones de página y los márgenes, puede usar el **GetProperties** método para recuperar los valores predeterminados:  
  
-   **PageHeight** y **PageWidth** especificar el alto de página predeterminado y el ancho. Cuando se inicia el control de impresión, los valores de estas propiedades se utilizan para seleccionar el tamaño de papel más cercano disponible para la impresora actualmente seleccionada. Si **PageWidth** es mayor que **PageHeight**, se establece la orientación en horizontal. De lo contrario, se establece en Vertical.  
  
-   **LeftMargin**, **RightMargin**, **TopMargin**, y **BottomMargin** están establecidos en 12,2 milímetros de forma predeterminada.  
  
 Estas propiedades se almacenan en la **elemento** colección de propiedades del servidor de informes. Los valores se sobrescriben cada vez que se actualiza una definición de informe.  
  
### <a name="rsclientprint-properties"></a>Propiedades de RSClientPrint  
  
|Propiedad|Tipo|RW|Valor de DB-Library|Description|  
|--------------|----------|--------|-------------|-----------------|  
|MarginLeft|Doble|RW|Valor del informe|Obtiene o establece el margen izquierdo. El valor predeterminado, si no lo ha establecido el desarrollador de software o no está especificado en el informe, es 12,2 milímetros.|  
|MarginRight|Doble|RW|Valor del informe|Obtiene o establece el margen derecho. El valor predeterminado, si no lo ha establecido el desarrollador de software o no está especificado en el informe, es 12,2 milímetros.|  
|MarginTop|Doble|RW|Valor del informe|Obtiene o establece el margen superior. El valor predeterminado, si no lo ha establecido el desarrollador de software o no está especificado en el informe, es 12,2 milímetros.|  
|MarginBottom|Doble|RW|Valor del informe|Obtiene o establece el margen inferior. El valor predeterminado, si no lo ha establecido el desarrollador de software o no está especificado en el informe, es 12,2 milímetros.|  
|PageWidth|Doble|RW|Valor del informe|Obtiene o establece el ancho de página. El valor predeterminado si no está establecido por el desarrollador o la definición de informe es 215,9 milímetros.|  
|PageHeight|Doble|RW|Valor del informe|Obtiene o establece el alto de página. El valor predeterminado, si no lo ha establecido el desarrollador de software o no está incluido en la definición de informe, es 279,4 milímetros.|  
|Culture|Int32|RW|Configuración regional del explorador|Especifica el identificador de configuración regional (LCID). Este valor determina la unidad de medida para la entrada del usuario. Por ejemplo, si un usuario escribe **3**, el valor se medirá en milímetros si el idioma es francés o pulgadas, si el idioma es el inglés (Estados Unidos). Los valores válidos son: 1028, 1031, 1033, 1036, 1040, 1041, 1042, 2052 y 3082.|  
|UICulture|String|RW|Valor de cultura del cliente|Especifica la traducción de las cadenas del cuadro de diálogo. El texto del cuadro de diálogo Imprimir está traducido a los idiomas que se indican a continuación: alemán, chino simplificado, chino tradicional, coreano, español, francés, inglés, italiano y japonés. Los valores válidos son: 1028, 1031, 1033, 1036, 1040, 1041, 1042, 2052 y 3082.|  
|Authenticate|Boolean|RW|False|Especifica si el control envía un comando GET en el servidor de informes para iniciar una conexión para la impresión fuera de sesión.|  
  
### <a name="when-to-set-the-authenticate-property"></a>Cuándo establecer la propiedad Authenticate  
 Al imprimir desde dentro de una sesión de explorador, no es necesario establecer la **Authenticate** propiedad. En el contexto de una sesión activa, todas las solicitudes del control de impresión que se hacen al servidor de informes se controlan a través del propio explorador. El explorador establece las variables de sesión necesarias para la comunicación con el servidor de informes.  
  
 Si imprime fuera de sesión (por ejemplo, enviar un informe directamente a una impresora sin abrirlo), el control de impresión debe emitir un HTTP **obtener** solicitud para configurar la sesión con el servidor de informes. Para emitir el **obtener** solicitar, establece **Authenticate** a **True**.  
  
 Solo debe emitir el **obtener** solicitud si usas Windows integrado seguridad o autenticación básica. Si utiliza autenticación de formularios, el **Authenticate** propiedad se omite. El código de la aplicación debe establecer la sesión y autenticar el usuario mediante la extensión de seguridad personalizada proporcionada. Si se utiliza la autenticación de formularios, es necesario establecer el valor de expiración de la cookie de autenticación en un valor que conserve las sesiones durante un periodo de tiempo razonable. Si el valor es demasiado bajo, se pedirá los usuarios que proporcionen las credenciales de inicio de sesión cada vez que expire la cookie.  
  
### <a name="clsids"></a>CLSID  
 Cuando ejecute el informe local, use los siguientes valores de CLSID.  
  
-   41861299-EAB2-4DCC-986C-802AE12AC499  
  
-   5554DCB0-700B-498D-9B58-4E40E5814405  
  
-   60677965-AB8B-464f-9B04-4BA871A2F17F  
  
 Cuando ejecute el informe en Windows Azure SQL Reporting, use los siguientes valores de CLSID.  
  
-   3DD32426-554D-48C0-A200-65D3BF880E38  
  
-   05662494-ACF9-446A-BE4C-7D3F7EA7F62F  
  
### <a name="rsprintclient-support-for-the-print-method"></a>Compatibilidad de RSPrintClient con el método Print  
 El **RSClientPrint** objeto admite el **impresión** método utilizado para iniciar el cuadro de diálogo de impresión. El **impresión** método tiene los siguientes argumentos.  
  
|Argumento|E/S|Tipo|Description|  
|--------------|----------|----------|-----------------|  
|ServerPath|Entrada|String|Especifica el directorio virtual del servidor de informes (por ejemplo, `https://adventure-works/reportserver`).|  
|ReportPathParameters|Entrada|String|Especifica el nombre completo para obtener acceso al informe en el espacio de nombres de carpetas del servidor de informes, incluidos los parámetros. Los informes se recuperan mediante el acceso a una dirección URL. Por ejemplo, "/AdventureWorks Sample Reports/Employee Sales Summary&EmpID=1234"|  
|ReportName|Entrada|String|Nombre corto del informe (en el ejemplo anterior, el nombre corto es Employee Sales Summary). Aparece en el cuadro de diálogo Imprimir y en la cola de impresión.|  
  
### <a name="example"></a>Ejemplo  
 En el ejemplo de HTML siguiente se muestra cómo especificar el archivo .cab, **impresión** método y las propiedades en JavaScript:  
  
 `<BODY onload="Print()">`  
  
 `<OBJECT ID="RSClientPrint" CLASSID="CLSID: 5554DCB0-700B-498D-9B58-4E40E5814405D3" CODEBASE="<URL to the .CAB file>#Version=<your application version information>" VIEWASTEXT></OBJECT>`  
  
 `<script language="javascript">`  
  
 `function Print()`  
  
 `{`  
  
 `RSClientPrint.MarginLeft = 12.7;`  
  
 `RSClientPrint.MarginTop = 12.7;`  
  
 `RSClientPrint.MarginRight = 12.7;`  
  
 `RSClientPrint.MarginBottom = 12.7;`  
  
 `RSClientPrint.Culture = 1033;`  
  
 `RSClientPrint.UICulture = 9;`  
  
 `RSClientPrint.Print('http://localhost/rtm', '%2fEmployee_Sales_Summary&ReportMonth=6&ReportYear=2004&EmpID=20', 'Employee_Sales_Summary')`  
  
 `}`  
  
 `</script>`  
  
 `</BODY>`  
  
## <a name="see-also"></a>Vea también  
 [Imprimir informes desde un explorador con el Control de impresión &#40; El generador de informes y SSRS &#41;](../../../reporting-services/report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md)   
 [Imprimir informes &#40; El generador de informes y SSRS &#41;](../../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)   
 [Configuración de información de dispositivo de imagen](../../../reporting-services/image-device-information-settings.md)  
  
  
