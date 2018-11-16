---
title: Personalización de marca del portal web | Microsoft Docs
ms.date: 11/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.openlocfilehash: fd469eb38d23a72037ab34dc6cceb45da39411a6
ms.sourcegitcommit: 9ece10c2970a4f0812647149d3de2c6b75713e14
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/16/2018
ms.locfileid: "51812998"
---
# <a name="branding-the-web-portal"></a>Personalización de marca del portal web

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

Puede modificar la apariencia del portal web personalizándolo con la marca de su empresa. Esto se realiza mediante un paquete de marca. El paquete de marca se ha diseñado de forma que no deba estar muy familiarizado con las hojas de estilo CSS para crearlo.  
  
<iframe width="560" height="315" src="https://www.youtube.com/embed/m08kLuofwFA?list=PLv2BtOtLblH3F--8WmK9QcLbx6dV_lVkL" frameborder="0" allowfullscreen></iframe>  
   
## <a name="creating-the-brand-package"></a>Creación del paquete de marca
  
Un paquete de marca para Reporting Services se compone de tres elementos y se empaqueta como archivo ZIP.   
  
- colors.json  
- metadata.xml  
- logo.png (opcional)  
  
Los archivos deben tener los nombres especificados arriba. Sin embargo, el archivo ZIP puede tener el nombre que quiera.  
  
### <a name="metadataxml"></a>metadata.xml
  
El archivo metadata.xml permite establecer el nombre del paquete de marca y presenta una entrada de referencia para los archivos colors.json y logo.png.  
  
Para modificar el nombre del paquete de marca, cambie el valor del atributo **name** del elemento **SystemResourcePackage** .  
  
    name="Multicolored example brand"  
  
También puede incluir una imagen de logotipo en el paquete de marca. Este elemento aparecerá dentro de Contents.  
  
Ejemplo sin un archivo de logotipo.  
  
    <Contents>  
      <Item key="colors" path="colors.json" />  
    </Contents>  
  
Ejemplo con un archivo de logotipo.  
  
    <Contents>  
      <Item key="colors" path="colors.json" />  
      <Item key="logo" path="logo.png" />  
    </Contents>  
  
### <a name="colorsjson"></a>colors.json
  
Cuando se carga el paquete de marca, el servidor extrae los pares nombre-valor del archivo colors.json y los combina con la hoja de estilos LESS maestra, brand.less. Después, este archivo LESS se procesa y el archivo CSS resultante se envía al cliente. Todos los colores de la hoja de estilos siguen la representación hexadecimal de seis caracteres de un color.  
  
La hoja de estilos LESS contiene bloques que hacen referencia a algunas variables LESS predefinidas, como las siguientes:  
  
    /* primary buttons */   
    .btn-primary {   
        color:@primaryButtonColor;   
        background-color:@primaryButtonBg;   
    }  
  
Aunque se parece a la sintaxis CSS, los valores de color, que llevan @symbol como prefijo, son exclusivos de LESS. Se trata de variables cuyo valor lo establece el archivo JSON.  
  
Por ejemplo, si el archivo colors.json tiene los siguientes valores:  
  
    "primary":"#009900",   
    "primaryContrast":"#ffffff"   
  
El resultado procesado buscaría la variable de LESS **@primaryButtonBg** y vería que está asignada a una propiedad de JSON llamada **primary**, que en este ejemplo es #009900. Por lo tanto, generaría el CSS correcto.  
  
    .btn-primary {   
        color:#ffffff;   
        background-color:#009900;   
    }  
  
Todos los botones principales se representarían en verde oscuro con el texto en blanco.  
  
Para Reporting Services, el archivo colors.json tiene dos categorías principales en las que se agrupan los elementos.  
  
- **interface**: incluye los elementos específicos del portal web de Reporting Services.  
- **theme**: incluye los elementos específicos de los informes móviles que cree.  
  
La sección interface se desglosa en las siguientes agrupaciones:  
  
|Sección|Descripción|  
|---|---|  
|primary|Colores de los botones y de desplazamiento.|  
|Secundario|Color de la barra de título, la barra de búsqueda, el menú izquierdo (si se muestra) y el texto.|  
|neutralPrimary|Fondos del área del informe y de inicio.|  
|neutralSecondary|Fondos de opciones de carpeta y cuadro de texto, así como del menú de configuración.|  
|neutralTertiary|Fondos de la configuración del sitio.|  
|Mensajes de peligro (danger), advertencia (warning) y operación correcta (success)|Colores de esos mensajes.|  
|KPI|Controla los colores para KPI buenos (1), neutrales (0), neutrales (-1) y ninguno.|  
  
La primera vez que se conecte con el Publicador de informes móviles a un servidor que tenga implementado un paquete de marca, se agregará el tema a los temas disponibles en el menú de la esquina superior derecha de la aplicación.  
  
![ssRSBrandingMobileReportPublisher](../reporting-services/media/ssrsbrandingmobilereportpublisher.png)  
  
Después, puede utilizar este tema para los informes móviles que cree, aunque no estén destinados al mismo servidor donde tenga implementado dicho tema.   
  
### <a name="using-a-logo"></a>Uso de un logotipo
  
Si incluye un logotipo en el paquete de marca, se mostrará en el portal web en lugar del nombre establecido para aquel en el menú Configuración del sitio.  
  
El archivo que incluya para el logotipo debe presentar el formato PNG. Las dimensiones del archivo se adaptarán una vez que se cargue al servidor. Se adaptarán para que presenten unos valores de unos 290 x 60 píxeles.  
   
## <a name="applying-the-brand-package-to-the-web-portal"></a>Aplicación del paquete de la marca al portal web
  
Para agregar, descargar o quitar un paquete de marca, puede hacer lo siguiente:  
  
1.  Seleccione el icono de **engranaje** de la esquina superior derecha.  
  
2.  Seleccione **Configuración del sitio**.  
  
    ![ssRSGearMenu](../reporting-services/media/ssrsgearmenu.png)  
  
3.  Seleccione **Branding**(Personalización de marca).  
  
    ![ssRSBranding](../reporting-services/media/ssrsbranding.png)  
  
En**Currently installed brand package** (Paquete de marca instalado actualmente) se mostrará el nombre del paquete que se ha cargado o Ninguno.  
  
La opción**Upload brand package** (Cargar paquete de marca) aplicará el paquete al portal web. Verá que los cambios surten efecto de inmediato.  
  
También puede **descargarse** o **quitar** el paquete. Si quita el paquete, se restablecerá inmediatamente el portal web a la marca predeterminada.  
  
## <a name="metadataxml-example"></a>Ejemplo de metadata.xml
  
    <?xml version="1.0" encoding="utf-8"?>  
    <SystemResourcePackage xmlns="https://schemas.microsoft.com/sqlserver/reporting/2016/01/systemresourcepackagemetadata"  
        type="UniversalBrand"  
        version="2.0.2"  
        name="Multicolored example brand"  
        >  
        <Contents>  
            <Item key="colors" path="colors.json" />  
            <Item key="logo" path="logo.png" />  
        </Contents>  
    </SystemResourcePackage>  
   
## <a name="colorsjson-example"></a>Ejemplo de colors.json
  
    {  
        "name":"Multicolored example brand",  
        "version":"1.0",  
        "interface":{  
            "primary":"#b31e1e",  
            "primaryAlt":"#ca0806",  
            "primaryAlt2":"#621013",  
            "primaryAlt3":"#e40000",  
            "primaryAlt4":"#e14e50",  
            "primaryContrast":"#fff",  
  
            "secondary":"#042200",  
            "secondaryAlt":"#0f4400",  
            "secondaryAlt2":"#155500",  
            "secondaryAlt3":"#217700",  
            "secondaryContrast":"#49e63c",  
  
            "neutralPrimary":"#d8edff",  
            "neutralPrimaryAlt":"#c9e6ff",  
            "neutralPrimaryAlt2":"#aedaff",  
            "neutralPrimaryAlt3":"#88c8ff",  
            "neutralPrimaryContrast":"#0a2b4c",  
  
            "neutralSecondary":"#e9d8eb",  
            "neutralSecondaryAlt":"#d9badc",  
            "neutralSecondaryAlt2":"#b06cb5",  
            "neutralSecondaryAlt3":"#a75bac",  
            "neutralSecondaryContrast":"#250a26",  
  
            "neutralTertiary":"#f79220",  
            "neutralTertiaryAlt":"#f8a54b",  
            "neutralTertiaryAlt2":"#facc9b",  
            "neutralTertiaryAlt3":"#fce3c7",  
            "neutralTertiaryContrast":"#391d00",  
  
            "danger":"#ff0000",  
            "success":"#00ff00",  
            "warning":"#ff8800",  
            "info":"#00ff",  
            "dangerContrast":"#fff",  
            "successContrast":"#fff",  
            "warningContrast":"#fff",  
            "infoContrast":"#fff",  
  
            "kpiGood":"#4fb443",  
            "kpiBad":"#de061a",  
            "kpiNeutral":"#d9b42c",  
            "kpiNone":"#333",  
            "kpiGoodContrast":"#fff",  
            "kpiBadContrast":"#fff",  
            "kpiNeutralContrast":"#fff",  
            "kpiNoneContrast":"#fff"  
           },  
           "theme":{  
            "dataPoints":[  
                "#0072c6",  
                "#f68c1f",  
                "#269657",  
                "#dd5900",  
                "#5b3573",  
                "#22bdef",  
                "#b4009e",  
                "#008274",  
                "#fdc336",  
                "#ea3c00",  
                "#00188f",  
                "#9f9f9f"  
            ],  
  
            "good":"#85ba00",  
            "bad":"#e90000",  
            "neutral":"#edb327",  
            "none":"#333",  
  
            "background":"#fff",  
            "foreground":"#222",  
            "mapBase":"#00aeef",  
            "panelBackground":"#f6f6f6",  
            "panelForeground":"#222",  
            "panelAccent":"#00aeef",  
            "tableAccent":"#00aeef",  
  
            "altBackground":"#f6f6f6",  
            "altForeground":"#000",  
            "altMapBase":"#f68c1f",  
            "altPanelBackground":"#235378",  
            "altPanelForeground":"#fff",  
            "altPanelAccent":"#fdc336",  
            "altTableAccent":"#fdc336"  
        }  
    }  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
