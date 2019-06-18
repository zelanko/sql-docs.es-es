---
title: Configuración de la información del dispositivo HTML | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- HTML [Reporting Services], rendering
- device information settings [Reporting Services], HTML rendering
ms.assetid: f505f478-dd6d-444a-957c-34f7cfb98911
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7c0d477364c4920e8220aef96629b24e34650ebb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65503100"
---
# <a name="html-device-information-settings"></a>Configuración de la información del dispositivo HTML
En la tabla siguiente se muestra la configuración de la información de los dispositivos para la representación en formato HTML.  
  
> [!IMPORTANT]  
>  La configuración de información de dispositivo que aparece en la siguiente tabla con **(\*)** está en desuso y no se debe usar en nuevas aplicaciones. Para más información, vea [Características obsoletas de SQL Server Reporting Services en SQL Server 2016](../reporting-services/deprecated-features-in-sql-server-reporting-services-ssrs.md)   
  
|Configuración|Valor|  
|-------------|-----------|  
|**AccessibleTablix**|Indica si se representa con metadatos de accesibilidad adicional para los usuarios con lectores verdes. Los metadatos de accesibilidad adicional provocan que el informe representado sea compatible con los siguientes estándares técnicos de la sección sobre información y aplicaciones de Internet y de la intranet basada en web (1194.22) del documento sobre estándares de accesibilidad de la tecnología de la información y la electrónica (sección 508):<br /><br /> (g) Los encabezados de fila y de columna se identificarán para las tablas de datos.<br /><br /> (h) Se usará marcado para asociar las celdas de datos y sus encabezados de las tablas que tengan dos o más niveles lógicos de encabezados de fila o columna.|  
|**ActionScript(\*)**|Especifica el nombre de la función JavaScript que se usará cuando se produzca un evento de acción, como una obtención de detalles o un clic en un marcador. Si se especifica este parámetro, un evento de acción desencadenará la función JavaScript la con nombre en lugar de una devolución al servidor.|  
|**BookmarkID**|Identificador del marcador al que saltar en el informe.|  
|**DocMap**|Indica si mostrar u ocultar el mapa del documento de informe. El valor predeterminado de este parámetro es **true**.|  
|**ExpandContent**|Indica si el informe se debería incluir en una estructura de tabla que restrinja el tamaño horizontal.|  
|**FindString**|Texto que se va a buscar en el informe. El valor predeterminado de este parámetro es una cadena vacía.|  
|**GetImage (\*)**|Obtiene un icono determinado para la interfaz de usuario del Visor HTML.|  
|**HTMLFragment**|Indica si un fragmento HTML se crea en lugar de un documento HTML completo. Un fragmento HTML incluye el contenido del informe en un elemento TABLE y omite los elementos BODY y HTML. El valor predeterminado es **false**. Si está representando en HTML mediante el método **M:ReportExecution2005.ReportExecutionService.Render(System.String,System.String,System.String@,System.String@,System.String@, ReportExecution2005.Warning[]@,System.String[]@)** de la API de SOAP, debe establecer la información del dispositivo en **true** si está representando un informe con imágenes. Al representar utilizando SOAP con la propiedad **HTMLFragment** establecida en **true** , se crean direcciones URL que contienen información de sesión que se puede utilizar para solicitar las imágenes correctamente. Las imágenes deben ser recursos cargados en la base de datos del servidor de informes.|  
|**ImageConsolidation**|Indica si se consolidan las imágenes de gráficos, mapas, medidores e indicadores representadas en una imagen grande. La consolidación de imágenes ayuda a mejorar el rendimiento del informe en el explorador de cliente cuando el informe contenga muchos elementos de visualización de datos. El valor predeterminado es **true** para la mayoría de los exploradores modernos.|  
|**JavaScript**|Indica si JavaScript se admite en el informe representado. El valor predeterminado es **true**.|  
|**LinkTarget**|Destino para los hipervínculos en el informe. El destino puede ser una ventana o un marco si se proporciona el nombre de la ventana, como **LinkTarget**=*nombre_ventana*o una ventana nueva si se usa **LinkTarget**=_blank. Otros nombres de destino válidos incluyen _self, _parent y _top.|  
|**OnlyVisibleStyles(\*)**|Indica que solo se generan los estilos compartidos para la página representada actualmente.|  
|**OutlookCompat**|Indica si la representación se va a realizar con metadatos adicionales que hacen que el informe tenga una apariencia mejorada en Outlook. Para las demás, el valor predeterminado es **false**.|  
|**Parámetros**|Indica si mostrar u ocultar el área de parámetros de la barra de herramientas. Si establece este parámetro en el valor **true**, se muestra el área de parámetros de la barra de herramientas. El valor predeterminado de este parámetro es **true**.|  
|**PrefixId**|Cuando se usa con **HTMLFragment**, agrega el prefijo especificado a todos los atributos **ID** del fragmento HTML creado.|  
|**ReplacementRoot(\*)**|La cadena que se agrega como prefijo a todos los vínculos de obtención de detalles, alternancia y marcador del informe cuando la representación se realice fuera del control ReportViewer. Se usa, por ejemplo, para redirigir el clic de un usuario a una página personalizada.|  
|**ResourceStreamRoot(\*)**|La cadena que se antepone a la dirección URL para todos los recursos de imagen, por ejemplo, las imágenes que se van a alternar u ordenar.|  
|**Sección**|Número de página del informe que representar. El valor **0** indica que se representan todas las secciones del informe. El valor predeterminado es **1**.|  
|**StreamRoot (\*)**|Ruta de acceso que se usa como prefijo para el valor del atributo **src** del elemento IMG en el informe HTML que devuelve el servidor de informes. De forma predeterminada, el servidor de informes proporciona la ruta de acceso. Puede usar este valor para especificar una ruta de acceso raíz para las imágenes de un informe (por ejemplo, **https://\<nombreDeServidor>/resources/companyimages**).|  
|**StyleStream**|Indica si los estilos y scripts se crean como un flujo independiente en lugar de en el documento. El valor predeterminado es **false**.|  
|**Barra de herramientas**|Indica si mostrar u ocultar la barra de herramientas. El valor predeterminado de este parámetro es **true**. Si el valor de este parámetro es **false**, se omiten todas las opciones restantes (excepto el mapa del documento). Si omite este parámetro, la barra de herramientas se muestra automáticamente para los formatos de representación que lo admiten.<br /><br /> Al usar el acceso URL para representar un informe, se representa la barra de herramientas del Visor de informes. La barra de herramientas no se representa a través de la API SOAP. Sin embargo, la configuración de la información de dispositivos **Toolbar** afecta a la manera en que el informe se muestra al usar el método de SOAP **Render** . Si el valor de este parámetro es **true** al utilizar SOAP para representar en HTML, solo se representa la primera sección del informe. Si el valor es **false**, el informe HTML completo se representa como una página HTML única.|  
|**UserAgent**|Cadena **user-agent** del explorador que está realizando la solicitud; esta cadena se encuentra en la solicitud HTTP.|  
|**Zoom (\*)**|Valor de ampliación del informe como porcentaje entero o una constante de cadena. Los valores de cadena estándar incluyen **Page Width** y **Whole Page**. Las versiones de [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer anteriores a Internet Explorer 5.0 y todos los exploradores que no son de[!INCLUDE[msCoName](../includes/msconame-md.md)] omiten este parámetro. El valor predeterminado de este parámetro es **100**.|  
|**DataVisualizationFitSizing**|Indica el comportamiento de ajuste para la visualización de datos cuando se esté dentro de un Tablix. Esto incluye un gráfico, un medidor y un mapa.<br /><br /> Los valores posibles son **Aproximado** y **Exacto**.<br /><br /> El valor predeterminado es **Aproximado**. Si se quita el valor de configuración del archivo **rsreportserver.config** , el comportamiento predeterminado es **Exacto**.<br /><br /> Si se habilita **Exacto** , podría afectar al rendimiento porque el procesamiento necesario para determinar el tamaño exacto puede tardar más tiempo.|  
  
## <a name="see-also"></a>Consulte también  
 [Pasar la configuración de información de dispositivo a las extensiones de representación](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar los parámetros de extensión de representación en RSReportServer.Config](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referencia técnica &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
