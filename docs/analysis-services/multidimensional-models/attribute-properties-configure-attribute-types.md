---
title: Configurar tipos de atributos | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- time dimensions [Analysis Services]
- attributes [Analysis Services], types
- slowly changing dimensions
- account dimensions [Analysis Services]
- currency dimensions [Analysis Services]
- Type property
ms.assetid: c2c6a3da-555e-4362-a83f-88da28427520
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3a7d8d9405d27956eecef276ef9a5b80b1806667
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="attribute-properties---configure-attribute-types"></a>Propiedades de atributo: configurar los tipos de atributos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], tipos de atributos ayudan a clasificar un atributo en términos de funcionalidad empresarial. Existen muchos tipos de atributos que, en su mayor parte, se utilizan en las aplicaciones cliente para mostrar o admitir un atributo. No obstante, algunos tipos de atributos también tienen significado específico para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Por ejemplo, algunos tipos de atributos identifican atributos que representan períodos en diferentes calendarios para las dimensiones de tiempo.  
  
##  <a name="setting_attibute_types"></a> Establecer tipos de atributos  
 El valor de la propiedad **Type** de un atributo determina el tipo de atributo de dicho atributo. Distintos asistentes de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] establecen los tipos de atributos al definir dimensiones o atributos. Estos asistentes de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] también establecen los tipos de atributos al agregar funcionalidad a las dimensiones. Por ejemplo, el Asistente de Business Intelligence aplica varios tipos de atributo a los atributos en una dimensión cuando agrega inteligencia de cuentas para identificar atributos que contienen los nombres, códigos, números y estructuras de cuentas en la dimensión. El Asistente de Business Intelligence también utiliza tipos de atributo, por ejemplo para la conversión de moneda. Para más información, vea [Crear una dimensión de tipo moneda](../../analysis-services/multidimensional-models/database-dimensions-create-a-currency-type-dimension.md).  
  
 En las siguientes tablas se incluyen los tipos de atributos disponibles en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. En estas tablas se separan los tipos de atributos en las siguientes categorías:  
  
|Término|Definición|  
|----------|----------------|  
|[Tipos de atributos generales](#general_attribute_types)|Estos valores están disponibles para todos los atributos y solo existen para permitir la clasificación de atributos para fines de aplicaciones cliente.|  
|[Tipos de atributos de dimensión de cuenta](#account_dimension_attribute_types)|Estos valores identifican un atributo que pertenece a una dimensión de cuenta. Para más información sobre las dimensiones de cuenta, vea [Crear una cuenta financiera de una dimensión de tipo primario-secundario](../../analysis-services/multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md).|  
|[Tipos de atributos de dimensión de moneda](#currency_dimension_attribute_types)|Estos valores identifican un atributo que pertenece a una dimensión de moneda. Para más información sobre las dimensiones de moneda, vea [Crear una dimensión de tipo moneda](../../analysis-services/multidimensional-models/database-dimensions-create-a-currency-type-dimension.md).|  
|[Atributos de dimensión de variación lenta](#slowly_changing_dimension_attribute_types)|Estos valores identifican un atributo que pertenece a una dimensión variable lenta.|  
|[Atributos de dimensión de tiempo](#time_dimension_attribute_types)|Estos valores identifican un atributo que pertenece a una dimensión de tiempo. Para más información sobre las dimensiones de tiempo, vea [Crear una dimensión de tipo Date](../../analysis-services/multidimensional-models/database-dimensions-create-a-date-type-dimension.md).|  
  
###  <a name="general_attribute_types"></a> General Attribute Types  
  
|Valor de tipo de atributo|Description|  
|--------------------------|-----------------|  
|**Dirección**|Representa una dirección.|  
|**AddressBuilding**|Representa un identificador de edificio de una dirección.|  
|**AddressCity**|Representa una ciudad de una dirección.|  
|**AddressCountry**|Representa un país o región de una dirección.|  
|**AddressFax**|Representa un número de fax.|  
|**AddressFloor**|Representa un identificador de planta de una dirección.|  
|**AddressHouse**|Representa un número de casa de una dirección.|  
|**AddressPhone**|Representa un número de teléfono.|  
|**AddressQuarter**|Representa un barrio de una dirección.|  
|**AddressRoom**|Representa un identificador de habitación de una dirección.|  
|**AddressStateOrProvince**|Representa un estado o provincia de una dirección.|  
|**AddressStreet**|Representa una calle de una dirección.|  
|**AddressZip**|Representa un código postal de una dirección.|  
|**BomResource**|Representa un recurso para una lista de materiales (BOM).|  
|**Caption**|Representa un título.|  
|**CaptionAbbreviation**|Representa una abreviatura.|  
|**CaptionDescription**|Representa una descripción.|  
|**Canal**|Representa un canal.|  
|**City**|Representa una ciudad.|  
|**Compañía**|Representa una empresa.|  
|**Continente**|Representa un continente.|  
|**País**|Representa un país o región.|  
|**Condado**|Representa un condado.|  
|**CustomerGroup**|Representa un grupo de clientes.|  
|**CustomerHousehold**|Representa un núcleo de clientes.|  
|**Clientes**|Representa un cliente.|  
|**DateCanceled**|Representa una fecha de cancelación.|  
|**DateDuration**|Representa una duración.|  
|**DateEnded**|Representa una fecha final.|  
|**DateModified**|Representa una fecha de modificación.|  
|**DateStart**|Representa una fecha de inicio.|  
|**DeletedFlag**|Indica si un miembro se ha eliminado o debería eliminarse (con respecto a la funcionalidad empresarial).<br /><br /> Nota: [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no utiliza este tipo de atributo para determinar si se debería eliminar un miembro. En su lugar, este tipo de atributo lo utilizan las aplicaciones cliente solamente para fines de presentación.|  
|**FormattingColor**|Representa el color utilizado en el formato.|  
|**FormattingFont**|Representa la fuente utilizada en el formato.|  
|**FormattingFontEffects**|Representa los efectos de fuente utilizado en el formato.|  
|**FormattingFontSize**|Representa el tamaño de fuente utilizado en el formato.|  
|**FormattingOrder**|Representa el orden utilizado en el formato.|  
|**FormattingSubtotal**|Representa un subtotal.|  
|**GeoBoundaryBottom**|Representa el valor más bajo de un límite geográfico.|  
|**GeoBoundaryFront**|Representa el valor al frente de un límite geográfico.|  
|**GeoBoundaryLeft**|Representa el valor más a la izquierda de un límite geográfico.|  
|**GeoBoundaryPolygon**|Representa la definición de polígono de un límite geográfico.|  
|**GeoBoundaryRear**|Representa el valor más trasero de un límite geográfico.|  
|**GeoBoundaryRight**|Representa el valor más a la derecha de un límite geográfico.|  
|**GeoBoundaryTop**|Representa el valor más alto de un límite geográfico.|  
|**GeoCentroidX**|Representa un centroide de eje X para una región geográfica.|  
|**GeoCentroidY**|Representa un centroide de eje Y para una región geográfica.|  
|**GeoCentroidZ**|Representa un centroide de eje Z para una región geográfica.|  
|**ID**|Representa un identificador (Id.) o clave.|  
|**Imagen**|Representa una imagen en un formato gráfico no definido.|  
|**ImageBmp**|Representa una imagen en un formato gráfico de mapa de bits.|  
|**ImageGif**|Representa una imagen en un formato gráfico GIF.|  
|**ImageJpg**|Representa una imagen en un formato gráfico JPEG.|  
|**ImagePng**|Representa una imagen en un formato PNG (Portable Network Graphics).|  
|**ImageTiff**|Representa una imagen en un formato gráfico TIFF.|  
|**OrganizationalUnit**|Representa una unidad organizativa.|  
|**OrgTitle**|Representa un título organizativo.|  
|**PercentOwnership**|Representa un porcentaje de propiedad.|  
|**PercentVoteRight**|Representa un porcentaje de derechos a voto.|  
|**Person**|Representa una persona.|  
|**PersonContact**|Representa los datos de contacto para una persona.|  
|**PersonDemographic**|Representa la información demográfica para una persona.|  
|**PersonFirstName**|Representa el nombre de una persona.|  
|**PersonFullName**|Representa el nombre completo de una persona.|  
|**PersonLastName**|Representa los apellidos de una persona.|  
|**PersonMiddleName**|Representa el segundo nombre de una persona.|  
|**PhysicalColor**|Representa un color.|  
|**PhysicalDensity**|Representa la densidad.|  
|**PhysicalDepth**|Representa la profundidad.|  
|**PhysicalHeight**|Representa el alto.|  
|**PhysicalSize**|Representa el tamaño.|  
|**PhysicalVolume**|Representa el volumen.|  
|**PhysicalWeight**|Representa el peso.|  
|**PhysicalWidth**|Representa el ancho.|  
|**Punto**|Representa un punto.|  
|**PostalCode**|Representa un código postal.|  
|**Product**|Representa un producto.|  
|**ProductBrand**|Representa una marca de producto.|  
|**ProductCategory**|Representa una categoría de producto.|  
|**ProductGroup**|Representa un grupo de productos.|  
|**ProductSKU**|Representa la referencia de almacén (SKU) de un producto.|  
|**Proyecto**|Representa un proyecto.|  
|**ProjectCode**|Representa un código de proyecto.|  
|**ProjectCompletion**|Representa el estado de finalización de un proyecto.|  
|**ProjectEndDate**|Representa una pestaña de fin de proyecto.|  
|**ProjectName**|Representa un nombre de proyecto.|  
|**ProjectStartDate**|Representa una fecha de inicio de proyecto.|  
|**Promoción**|Representa una promoción.|  
|**QtyRangeHigh**|Representa el valor más alto de un intervalo de cantidades.|  
|**QtyRangeLow**|Representa el valor más bajo de un intervalo de cantidades.|  
|**Cuantitativo**|Representa un atributo cuantitativo.|  
|**Rate**|Representa una tasa o tarifa.|  
|**RateType**|Representa un tipo de tasa o tarifa.|  
|**Region**|Representa una región definida por el cliente.|  
|**Regular**|Representa un atributo normal.|  
|**RelationToParent**|Representa una relación con un elemento primario.|  
|**Representative**|Representa un representante.|  
|**Escenario**|Representa un escenario.|  
|**Secuencia**|Representa un atributo de secuencia.|  
|**ShortCaption**|Representa un título corto.|  
|**StateOrProvince**|Representa un estado o provincia.|  
|**Utilidad**|Representa una utilidad.|  
|**Versión**|Representa una versión.|  
|**WebHtml**|Representa contenido HTML.|  
|**WebMailAlias**|Representa un alias de correo electrónico.|  
|**WebUrl**|Representa una dirección URL.|  
|**WebXmlOrXsl**|Representa contenido XML o XSL.|  
  
###  <a name="account_dimension_attribute_types"></a> Account Dimension Attribute Types  
  
|Valor de tipo de atributo|Description|  
|--------------------------|-----------------|  
|**Cuenta**|Representa el elemento primario de una cuenta. Este tipo de atributo se suele aplicar al atributo primario de una dimensión de cuenta.|  
|**AccountName**|Representa el nombre de una cuenta. Este tipo de atributo se suele aplicar a los atributos de clave de una dimensión de cuenta.|  
|**AccountNumber**|Representa el número de una cuenta.|  
|**AccountType**|Representa el tipo de una cuenta. Este tipo de atributo identifica la función de agregación de un miembro de la cuenta de una dimensión de tipo de cuenta de la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
  
###  <a name="currency_dimension_attribute_types"></a> Tipos de atributos de dimensión de moneda  
  
|Valor de tipo de atributo|Description|  
|--------------------------|-----------------|  
|**CurrencyDestination**|Representa la moneda de destino de un cambio de divisas. Este tipo de atributo se suele aplicar al atributo clave de una dimensión de informe, para su uso en la conversión de moneda. Para más información sobre las conversiones de moneda, vea [Conversiones de moneda &#40;Analysis Services&#41;](../../analysis-services/currency-conversions-analysis-services.md).|  
|**CurrencyIsoCode**|Representa el código ISO (International Standards Organization) de una moneda. Para más información sobre las conversiones de moneda, vea [Conversiones de moneda &#40;Analysis Services&#41;](../../analysis-services/currency-conversions-analysis-services.md).|  
|**CurrencyName**|Representa el nombre de una moneda. Para más información sobre las conversiones de moneda, vea [Conversiones de moneda &#40;Analysis Services&#41;](../../analysis-services/currency-conversions-analysis-services.md).|  
|**CurrencySource**|Representa la moneda de origen de un cambio de divisas. Este tipo de atributo se suele aplicar al atributo clave de una dimensión de moneda, para su uso en la conversión de monedas. Para más información sobre las conversiones de moneda, vea [Conversiones de moneda &#40;Analysis Services&#41;](../../analysis-services/currency-conversions-analysis-services.md).|  
  
###  <a name="slowly_changing_dimension_attribute_types"></a> Tipos de atributos de dimensión variable lenta  
  
|Valor de tipo de atributo|Description|  
|--------------------------|-----------------|  
|**ScdEndDate**|Representa la fecha final efectiva para un miembro en una dimensión variable lenta.|  
|**ScdOriginalID**|Representa el identificador original para un miembro en una dimensión variable lenta.|  
|**ScdStartDate**|Representa la fecha de inicio efectiva para un miembro en una dimensión variable lenta.|  
|**ScdStatus**|Representa el estado efectivo para un miembro en una dimensión variable lenta.|  
  
###  <a name="time_dimension_attribute_types"></a> Tipos de atributos de dimensión de tiempo  
  
|Valor de tipo de atributo|Description|  
|--------------------------|-----------------|  
|**Date**|Representa una fecha. Este tipo de atributo se suele aplicar al atributo clave de una dimensión de tiempo o de tiempo de servidor.|  
|**DayOfHalfYear**|Representa el ordinal del día de un semestre.|  
|**DayOfMonth**|Representa el ordinal del día de un mes.|  
|**DayOfQuarter**|Representa el ordinal del día de un trimestre.|  
|**DayOfTenDays**|Representa el ordinal del día de un período de diez días.|  
|**DayOfTrimester**|Representa el ordinal del día de un cuatrimestre.|  
|**DayOfWeek**|Representa el ordinal del día de una semana.|  
|**DayOfYear**|Representa el ordinal del día de un año.|  
|**Días**|Representa los días.|  
|**FiscalDate**|Representa una fecha en un calendario fiscal.|  
|**FiscalDayOfHalfYear**|Representa el ordinal del día de un semestre en un calendario fiscal.|  
|**FiscalDayOfMonth**|Representa el ordinal del día de un mes en un calendario fiscal.|  
|**FiscalDayOfQuarter**|Representa el ordinal del día de un trimestre en un calendario fiscal.|  
|**FiscalDayOfTrimester**|Representa el ordinal del día de un cuatrimestre en un calendario fiscal.|  
|**FiscalDayOfWeek**|Representa el ordinal del día de una semana en un calendario fiscal.|  
|**FiscalDayOfYear**|Representa el ordinal del día de un año en un calendario fiscal.|  
|**FiscalHalfYears**|Representa los semestres en un calendario fiscal.|  
|**FiscalHalfYearOfYear**|Representa el ordinal del semestre de un año en un calendario fiscal.|  
|**FiscalMonths**|Representa los meses en un calendario fiscal.|  
|**FiscalMonthOfHalfYear**|Representa el ordinal del mes de un semestre en un calendario fiscal.|  
|**FiscalMonthOfQuarter**|Representa el ordinal del mes de un trimestre en un calendario fiscal.|  
|**FiscalMonthOfTrimester**|Representa el ordinal del mes de un cuatrimestre en un calendario fiscal.|  
|**FiscalMonthOfYear**|Representa el ordinal del mes de un año en un calendario fiscal.|  
|**FiscalQuarters**|Representa los trimestres en un calendario fiscal.|  
|**FiscalQuarterOfHalfYear**|Representa el ordinal del trimestre de un semestre en un calendario fiscal.|  
|**FiscalQuarterOfYear**|Representa el ordinal del trimestre de un año en un calendario fiscal.|  
|**FiscalTrimesters**|Representa los cuatrimestres en un calendario fiscal.|  
|**FiscalTrimesterOfYear**|Representa el ordinal del cuatrimestre de un año en un calendario fiscal.|  
|**FiscalWeeks**|Representa las semanas en un calendario fiscal.|  
|**FiscalWeekOfHalfYear**|Representa el ordinal de la semana de un semestre en un calendario fiscal.|  
|**FiscalWeekOfMonth**|Representa el ordinal de la semana de un mes en un calendario fiscal.|  
|**FiscalWeekOfQuarter**|Representa el ordinal de la semana de un trimestre en un calendario fiscal.|  
|**FiscalWeekOfTrimester**|Representa el ordinal de la semana de un cuatrimestre en un calendario fiscal.|  
|**FiscalWeekOfYear**|Representa el ordinal de la semana de un año en un calendario fiscal.|  
|**FiscalYears**|Representa los años en un calendario fiscal.|  
|**HalfYears**|Representa los semestres.|  
|**HalfYearOfYear**|Representa el ordinal del semestre de un año.|  
|**Horas**|Representa las horas.|  
|**IsHoliday**|Indica si la fecha es un día festivo.|  
|**ISO8601Date**|Representa una fecha en un calendario ISO 8601.|  
|**ISO8601DayOfWeek**|Representa el ordinal del día de una semana en un calendario ISO 8601.|  
|**ISO8601DayOfYear**|Representa el ordinal del día de un año en un calendario ISO 8601.|  
|**ISO8601Weeks**|Representa las semanas en un calendario ISO 8601.|  
|**ISO8601WeekOfYear**|Representa el ordinal de la semana de un año en un calendario ISO 8601.|  
|**ISO8601Years**|Representa los años en un calendario ISO 8601.|  
|**IsPeakDay**|Indica si una fecha es un día pico.|  
|**IsWeekDay**|Indica si una fecha es un día de la semana.|  
|**IsWorkingDay**|Indica si una fecha es un día laborable.|  
|**ManufacturingDate**|Representa una fecha en un calendario de fabricación.|  
|**ManufacturingDayOfHalfYear**|Representa el ordinal del día de un semestre en un calendario de fabricación.|  
|**ManufacturingDayOfMonth**|Representa el ordinal del día de un mes en un calendario de fabricación.|  
|**ManufacturingDayOfQuarter**|Representa el ordinal del día de un trimestre en un calendario de fabricación.|  
|**ManufacturingDayOfTrimester**|Representa el ordinal del día de un cuatrimestre en un calendario de fabricación.|  
|**ManufacturingDayOfWeek**|Representa el ordinal del día de una semana en un calendario de fabricación.|  
|**ManufacturingDayOfYear**|Representa el ordinal del día de un año en un calendario de fabricación.|  
|**ManufacturingHalfYears**|Representa los semestres en un calendario de fabricación.|  
|**ManufacturingHalfYearOfYear**|Representa el ordinal del semestre de un año en un calendario de fabricación.|  
|**ManufacturingMonths**|Representa los meses en un calendario de fabricación.|  
|**ManufacturingMonthOfHalfYear**|Representa el ordinal del mes de un semestre en un calendario de fabricación.|  
|**ManufacturingMonthOfQuarter**|Representa el ordinal del mes de un trimestre en un calendario de fabricación.|  
|**ManufacturingMonthOfTrimester**|Representa el ordinal del mes de un cuatrimestre en un calendario de fabricación.|  
|**ManufacturingMonthOfYear**|Representa el ordinal del mes de un año en un calendario de fabricación.|  
|**ManufacturingQuarters**|Representa los trimestres en un calendario de fabricación.|  
|**ManufacturingQuarterOfHalfYear**|Representa el ordinal del trimestre de un semestre en un calendario de fabricación.|  
|**ManufacturingQuarterOfYear**|Representa el ordinal del trimestre de un año en un calendario de fabricación.|  
|**ManufacturingWeeks**|Representa las semanas en un calendario de fabricación.|  
|**ManufacturingWeekOfHalfYear**|Representa el ordinal de la semana de un semestre en un calendario de fabricación.|  
|**ManufacturingWeekOfMonth**|Representa el ordinal de la semana de un mes en un calendario de fabricación.|  
|**ManufacturingWeekOfQuarter**|Representa el ordinal de la semana de un trimestre en un calendario de fabricación.|  
|**ManufacturingWeekOfTrimester**|Representa el ordinal de la semana de un cuatrimestre en un calendario de fabricación.|  
|**ManufacturingWeekOfYear**|Representa el ordinal de la semana de un año en un calendario de fabricación.|  
|**ManufacturingYears**|Representa los años en un calendario de fabricación.|  
|**Minutos**|Representa los minutos.|  
|**Months**|Representa los meses.|  
|**MonthOfHalfYear**|Representa el ordinal del mes de un semestre.|  
|**MonthOfQuarter**|Representa el ordinal del mes de un trimestre.|  
|**MonthOfTrimester**|Representa el ordinal del mes de un cuatrimestre.|  
|**MonthOfYear**|Representa el ordinal del mes de un año.|  
|**Quarters**|Representa los cuatrimestres.|  
|**QuarterOfHalfYear**|Representa el ordinal del trimestre de un semestre.|  
|**QuarterOfYear**|Representa el ordinal del trimestre de un año.|  
|**ReportingDate**|Representa una fecha en un calendario de informes.|  
|**ReportingDayOfHalfYear**|Representa el ordinal del día de un semestre en un calendario de informes.|  
|**ReportingDayOfMonth**|Representa el ordinal del día de un mes en un calendario de informes.|  
|**ReportingDayOfQuarter**|Representa el ordinal del día de un trimestre en un calendario de informes.|  
|**ReportingDayOfTrimester**|Representa el ordinal del día de un cuatrimestre en un calendario de informes.|  
|**ReportingDayOfWeek**|Representa el ordinal del día de una semana en un calendario de informes.|  
|**ReportingDayOfYear**|Representa el ordinal del día de un año en un calendario de informes.|  
|**ReportingHalfYears**|Representa los semestres en un calendario de informes.|  
|**ReportingHalfYearOfYear**|Representa el ordinal del semestre de un año en un calendario de informes.|  
|**ReportingMonths**|Representa los meses en un calendario de informes.|  
|**ReportingMonthOfHalfYear**|Representa el ordinal del mes de un semestre en un calendario de informes.|  
|**ReportingMonthOfQuarter**|Representa el ordinal del mes de un trimestre en un calendario de informes.|  
|**ReportingMonthOfTrimester**|Representa el ordinal del mes de un cuatrimestre en un calendario de informes.|  
|**ReportingMonthOfYear**|Representa el ordinal del mes de un año en un calendario de informes.|  
|**ReportingQuarters**|Representa los trimestres en un calendario de informes.|  
|**ReportingQuarterOfHalfYear**|Representa el ordinal del trimestre de un semestre en un calendario de informes.|  
|**ReportingQuarterOfYear**|Representa el ordinal del trimestre de un año en un calendario de informes.|  
|**ReportingTrimesters**|Representa los cuatrimestres en un calendario de informes.|  
|**ReportingTrimesterOfYear**|Representa el ordinal del cuatrimestre de un año en un calendario de informes.|  
|**ReportingWeeks**|Representa las semanas en un calendario de informes.|  
|**ReportingWeekOfHalfYear**|Representa el ordinal de la semana de un semestre en un calendario de informes.|  
|**ReportingWeekOfMonth**|Representa el ordinal de la semana de un mes en un calendario de informes.|  
|**ReportingWeekOfQuarter**|Representa el ordinal de la semana de un trimestre en un calendario de informes.|  
|**ReportingWeekOfTrimester**|Representa el ordinal de la semana de un cuatrimestre en un calendario de informes.|  
|**ReportingWeekOfYear**|Representa el ordinal de la semana de un año en un calendario de informes.|  
|**ReportingYears**|Representa los años en un calendario de informes.|  
|**Segundos**|Representa los segundos.|  
|**TenDayOfHalfYear**|Representa el ordinal del período de diez días de un semestre.|  
|**TenDayOfMonth**|Representa el ordinal del período de diez días de un mes.|  
|**TenDayOfQuarter**|Representa el ordinal del período de diez días de un trimestre.|  
|**TenDayOfTrimester**|Representa el ordinal del período de diez días de un cuatrimestre.|  
|**TenDayOfYear**|Representa el ordinal del período de diez días de un año.|  
|**TenDays**|Representa los períodos de diez días.|  
|**Trimesters**|Representa los cuatrimestres.|  
|**TrimesterOfYear**|Representa el ordinal del cuatrimestre de un año.|  
|**UndefinedTime**|Representa un período de tiempo sin definir.|  
|**WeekOfYear**|Representa el ordinal de la semana de un año.|  
|**Weeks**|Representa las semanas.|  
|**WinterSummerSeason**|Indica si la fecha forma parte de la temporada de invierno o verano.|  
|**Years**|Representa los años|  
  
## <a name="see-also"></a>Vea también  
 [Atributos y jerarquías de atributos](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Referencia de las propiedades de los atributos de dimensión](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
