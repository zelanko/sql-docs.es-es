---
title: Tipo de elemento (DimensionAttribute) (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Type Element (DimensionAttribute)
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: TYPE
helpviewer_keywords: Type element
ms.assetid: 64fce1f5-39b7-4d0a-ae60-21203a03bd0d
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 35aef5d58cff864725f1ce483e7c623c58e5bcdd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="type-element-dimensionattribute-assl"></a>Elemento Type (DimensionAttribute) (ASSL)
  Contiene el tipo del atributo.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DimensionAttribute>  
      ...  
   <Type>...</Type>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Regular*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Cuenta*|El atributo representa el nombre de una cuenta.|  
|*AccountNumber*|El atributo representa el número de una cuenta.|  
|*AccountType*|El atributo representa el tipo de una cuenta.|  
|*Dirección*|El atributo representa una dirección.|  
|*AddressBuilding*|El atributo representa un identificador de edificio para una dirección.|  
|*AddressCity*|El atributo representa una ciudad para una dirección.|  
|*AddressCountry*|El atributo representa un país o región para una dirección.|  
|*AddressFax*|El atributo representa un número de teléfono del fax.|  
|*AddressFloor*|El atributo representa un identificador de planta para una dirección.|  
|*AddressHouse*|El atributo representa un número de casa para una dirección.|  
|*AddressPhone*|El atributo representa un número de teléfono.|  
|*AddressQuarter*|El atributo representa un barrio para una dirección.|  
|*AddressRoom*|El atributo representa una habitación para una dirección.|  
|*AddressStateOrProvince*|El atributo representa un estado o provincia para una dirección.|  
|*AddressStreet*|El atributo representa una calle para una dirección.|  
|*AddressZip*|El atributo representa un código postal para una dirección.|  
|*BOMResource*|El atributo representa un recurso para una lista de materiales (BOM).|  
|*Título*|El atributo representa un título.|  
|*CaptionAbbreviation*|El atributo representa una abreviatura.|  
|*CaptionDescription*|El atributo representa una descripción.|  
|*Canal*|El atributo representa un canal.|  
|*Ciudad*|El atributo representa una ciudad|  
|*Empresa*|El atributo representa una compañía.|  
|*Continente*|El atributo representa un continente.|  
|*País*|El atributo representa un país o región.|  
|*Condado*|El atributo representa un condado.|  
|*CurrencyDestination*|El atributo representa el destino de la moneda en un cambio de divisas.|  
|*CurrencyISOcode*|El atributo representa el código ISO de una divisa.|  
|*CurrencName*|El atributo representa el nombre de una divisa.|  
|*CurrencySource*|El atributo representa la divisa de origen de un cambio de divisas.|  
|*CustomerGroup*|El atributo representa un grupo de clientes.|  
|*CustomerHousehold*|El atributo representa un núcleo de clientes.|  
|*Clientes*|El atributo representa un cliente.|  
|*Date*|El atributo representa una fecha.|  
|*DateCanceled*|El atributo representa una fecha de cancelación.|  
|*DateDuration*|El atributo representa una duración.|  
|*DateEnded*|El atributo representa una fecha de finalización.|  
|*DateModified*|El atributo representa una fecha de modificación.|  
|*DateStart*|El atributo representa una fecha de inicio.|  
|*DayOfHalfYears*|El atributo representa el ordinal del día de un semestre.|  
|*DayOfMonth*|El atributo representa el ordinal del día de un mes.|  
|*DayOfQuarter*|El atributo representa el ordinal del día de un trimestre.|  
|*DayOfTrimester*|El atributo representa el ordinal del día de un cuatrimestre.|  
|*DayOfWeek*|El atributo representa el ordinal del día de una semana.|  
|*DayOfYear*|El atributo representa el ordinal del día de un año.|  
|*Días*|El atributo representa los días.|  
|*DaysOfTenDays*|El atributo representa el ordinal del día de un período de diez días.|  
|*FiscalDay*|El atributo representa los días en un calendario fiscal.|  
|*FiscalDayOfHalfYears*|El atributo representa el ordinal del día de un medio año en un calendario fiscal.|  
|*FiscalDayOfMonth*|El atributo representa el ordinal del día en un mes de un calendario fiscal.|  
|*FiscalDayOfQuarter*|El atributo representa el ordinal del día en un trimestre de un calendario fiscal.|  
|*FiscalDayOfTrimester*|El atributo representa el ordinal del día en un cuatrimestre de un calendario fiscal.|  
|*FiscalDayOfWeek*|El atributo representa el ordinal del día en una semana de un calendario fiscal.|  
|*FiscalDayOfYear*|El atributo representa el ordinal del día en un año de un calendario fiscal.|  
|*FiscalHalfYears*|El atributo representa los semestres de un calendario fiscal.|  
|*FiscalHalfYearsOfYear*|El atributo representa el ordinal del semestre en un año de un calendario fiscal.|  
|*Mes fiscal*|El atributo representa los meses de un calendario fiscal.|  
|*FiscalMonthOfHalfYears*|El atributo representa el ordinal del mes en un semestre de un calendario fiscal.|  
|*FiscalMonthOfQuarter*|El atributo representa el ordinal del mes en un trimestre de un calendario fiscal.|  
|*FiscalMonthOfTrimester*|El atributo representa el ordinal del mes en un cuatrimestre de un calendario fiscal.|  
|*FiscalMonthOfYear*|El atributo representa el ordinal del mes en un año de un calendario fiscal.|  
|*FiscalQuarter*|El atributo representa los trimestres de un calendario fiscal.|  
|*FiscalQuarterOfHalfYear*|El atributo representa el ordinal del trimestre en un semestre de un calendario fiscal.|  
|*FiscalQuarterOfYear*|El atributo representa el ordinal del trimestre en un año de un calendario fiscal.|  
|*FiscalTrimester*|El atributo representa los cuatrimestres de un calendario fiscal.|  
|*FiscalTrimesterOfYear*|El atributo representa el ordinal del cuatrimestre en un año de un calendario fiscal.|  
|*FiscalWeek*|El atributo representa las semanas de un calendario fiscal.|  
|*FiscalWeekOfHalfYears*|El atributo representa el ordinal de la semana en un semestre de un calendario fiscal.|  
|*FiscalWeekOfMonth*|El atributo representa el ordinal de la semana en un mes de un calendario fiscal.|  
|*FiscalWeekOfQuarter*|El atributo representa el ordinal de la semana en un trimestre de un calendario fiscal.|  
|*FiscalWeekOfTrimester*|El atributo representa el ordinal de la semana en un cuatrimestre de un calendario fiscal.|  
|*FiscalWeekOfYear*|El atributo representa el ordinal de la semana en un año de un calendario fiscal.|  
|*FiscalYear*|El atributo representa los años de un calendario fiscal.|  
|*FormattingColor*|El atributo representa el color usado en el formato.|  
|*FormattingFont*|El atributo representa la fuente usada en el formato.|  
|*FormattingFontEffects*|El atributo representa los efectos de fuente usados en el formato.|  
|*FormattingFontSize*|El atributo representa el tamaño de fuente usado en el formato.|  
|*FormattingOrder*|El atributo representa el orden usado en el formato.|  
|*FormattingSubtotal*|El atributo representa un subtotal.|  
|*GeoBoundaryBottom*|El atributo representa el valor más bajo de un límite geográfico.|  
|*GeoBoundaryFront*|El atributo representa el valor más frontal de un límite geográfico.|  
|*GeoBoundaryLeft*|El atributo representa el valor más a la izquierda de un límite geográfico.|  
|*GeoBoundaryPolygon*|El atributo representa la definición poligonal de un límite geográfico.|  
|*GeoBoundaryRear*|El atributo representa el valor más trasero de un límite geográfico.|  
|*GeoBoundaryRight*|El atributo representa el valor más a la derecha de un límite geográfico.|  
|*GeoBoundaryTop*|El atributo representa el valor más alto de un límite geográfico.|  
|*GeoCentroidX*|El atributo representa un centroide de eje X de una región geográfica.|  
|*GeoCentroidY*|El atributo representa un centroide de eje Y de una región geográfica.|  
|*GeoCentroidZ*|El atributo representa un centroide de eje Z de una región geográfica.|  
|*HalfYears*|El atributo representa los semestres.|  
|*HalfYearsOfYear*|El atributo representa el ordinal del semestre de un año.|  
|*Horas*|El atributo representa las horas.|  
|*Id.*|El atributo representa un identificador o clave.|  
|*IsHoliday*|El atributo indica si una fecha es un día no laborable.|  
|*ISO8601DayOfWeek*|El atributo representa el ordinal del día de una semana en un calendario ISO 8601.|  
|*ISO8601DayOfYear*|El atributo representa el ordinal del día en un año de un calendario ISO 8601.|  
|*ISO8601Days*|El atributo representa los días de un calendario ISO 8601.|  
|*ISO8601Week*|El atributo representa las semanas de un calendario ISO 8601.|  
|*ISO8601WeekOfYear*|El atributo representa el ordinal de la semana en un año de un calendario ISO 8601.|  
|*ISO8601Year*|El atributo representa los años en un calendario ISO 8601.|  
|*IsWeekDay*|El atributo indica si una fecha es un día de la semana.|  
|*IsWorkingDay*|El atributo indica si una fecha es un día laborable.|  
|*ManufacturingDay*|El atributo representa los días de un calendario de fabricación.|  
|*ManufacturingDayOfHalfYears*|El atributo representa el ordinal del día en un semestre de un calendario de fabricación.|  
|*ManufacturingDayOfMonth*|El atributo representa el ordinal del día en un mes de un calendario de fabricación.|  
|*ManufacturingDayOfQuarter*|El atributo representa el ordinal del día en un trimestre de un calendario de fabricación.|  
|*ManufacturingDayOfTrimester*|El atributo representa el ordinal del día en un cuatrimestre de un calendario de fabricación.|  
|*ManufacturingDayOfWeek*|El atributo representa el ordinal del día en una semana de un calendario de fabricación.|  
|*ManufacturingDayOfYear*|El atributo representa el ordinal del día en un año de un calendario de fabricación.|  
|*ManufacturingHalfYears*|El atributo representa los semestres de un calendario de fabricación.|  
|*ManufacturingHalfYearsOfYear*|El atributo representa el ordinal del semestre en un año de un calendario de fabricación.|  
|*ManufacturingMonth*|El atributo representa los meses de un calendario de fabricación.|  
|*ManufacturingMonthOfHalfYears*|El atributo representa el ordinal del mes en un semestre de un calendario de fabricación.|  
|*ManufacturingMonthOfQuarter*|El atributo representa el ordinal del mes en un trimestre de un calendario de fabricación.|  
|*ManufacturingMonthOfTrimester*|El atributo representa el ordinal del mes en un cuatrimestre de un calendario de fabricación.|  
|*ManufacturingMonthOfYear*|El atributo representa el ordinal del mes en un año de un calendario de fabricación.|  
|*ManufacturingQuarter*|El atributo representa los trimestres de un calendario de fabricación.|  
|*ManufacturingQuarterOfHalfYear*|El atributo representa el ordinal del trimestre en un semestre de un calendario de fabricación.|  
|*ManufacturingQuarterOfYear*|El atributo representa el ordinal del trimestre en un año de un calendario de fabricación.|  
|*ManufacturingTrimester*|El atributo representa los cuatrimestres de un calendario de fabricación.|  
|*ManufacturingTrimesterOfYear*|El atributo representa el ordinal del cuatrimestre en un año de un calendario de fabricación.|  
|*ManufacturingWeek*|El atributo representa las semanas de un calendario de fabricación.|  
|*ManufacturingWeekOfHalfYears*|El atributo representa el ordinal de la semana en un semestre de un calendario de fabricación.|  
|*ManufacturingWeekOfMonth*|El atributo representa el ordinal de la semana en un mes de un calendario de fabricación.|  
|*ManufacturingWeekOfQuarter*|El atributo representa el ordinal de la semana en un trimestre de un calendario de fabricación.|  
|*ManufacturingWeekOfTrimester*|El atributo representa el ordinal de la semana en un cuatrimestre de un calendario de fabricación.|  
|*ManufacturingWeekOfYear*|El atributo representa el ordinal de la semana en un año de un calendario de fabricación.|  
|*ManufacturingYear*|El atributo representa los años de un calendario de fabricación.|  
|*Minutos*|El atributo representa los minutos.|  
|*MonthOfHalfYears*|El atributo representa el ordinal del mes de un semestre.|  
|*MonthOfQuarter*|El atributo representa el ordinal del mes de un trimestre.|  
|*MonthOfTrimester*|El atributo representa el ordinal del mes de un cuatrimestre.|  
|*MonthOfYear*|El atributo representa el ordinal del mes de un año.|  
|*Meses*|El atributo representa los meses.|  
|*OrganizationalUnit*|El atributo representa una unidad organizativa.|  
|*OrgTitle*|El atributo representa un título organizativo.|  
|*PercentOwnership*|El atributo representa un porcentaje de propiedad.|  
|*PercentVoteRight*|El atributo representa un porcentaje de derechos de voto.|  
|*Persona*|El atributo representa una persona.|  
|*PersonContact*|El atributo representa información de contacto de una persona.|  
|*PersonDemographic*|El atributo representa la información demográfica para una persona.|  
|*PersonFirstName*|El atributo representa el nombre de pila (nombre) de una persona.|  
|*PersonFullName*|El atributo representa el nombre completo de una persona.|  
|*PersonLastName*|El atributo representa los apellidos de una persona.|  
|*PersonMiddleName*|El atributo representa el nombre completo de una persona.|  
|*PhysicalColor*|El atributo representa un color.|  
|*PhysicalDensity*|El atributo representa la densidad.|  
|*PhysicalDepth*|El atributo representa la profundidad.|  
|*PhysicalHeight*|El atributo representa el alto.|  
|*PhysicalSize*|El atributo representa el tamaño.|  
|*PhysicalVolume*|El atributo representa el volumen.|  
|*PhysicalWeight*|El atributo representa el peso.|  
|*PhysicalWidth*|El atributo representa el ancho.|  
|*Point*|El atributo representa un punto.|  
|*Código postal*|El atributo representa un código postal.|  
|*Product*|El atributo representa un producto.|  
|*ProductBrand*|El atributo representa una marca de producto.|  
|*ProductCategory*|El atributo representa una categoría de producto.|  
|*ProductGroup*|El atributo representa un grupo de productos.|  
|*ProductSKU*|El atributo representa la referencia de almacén (SKU) de un producto.|  
|*ProjectCode*|El atributo representa un código de proyecto.|  
|*Projectcompletion*|El atributo representa el estado de finalización de un proyecto.|  
|*ProjectEnddate*|El atributo representa una fecha de fin de proyecto.|  
|*Nombre de proyecto*|El atributo representa un nombre de proyecto.|  
|*ProjectStartDate*|El atributo representa una fecha de inicio de proyecto.|  
|*Promoción*|El atributo representa una promoción.|  
|*QtyRangeHigh*|El atributo representa el valor más alto de un intervalo de cantidades.|  
|*QtyRangeLow*|El atributo representa el valor más bajo de un intervalo de cantidades.|  
|*Cuantitativa*|El atributo representa un atributo cuantitativo.|  
|*QuarterOfHalfYear*|El atributo representa el ordinal del trimestre de un semestre.|  
|*QuarterOfYear*|El atributo representa el ordinal del trimestre de un año.|  
|*Trimestres*|El atributo representa los trimestres.|  
|*Velocidad*|El atributo representa una tarifa.|  
|*RateType*|El atributo representa un tipo de tarifa.|  
|*Region*|El atributo representa una región definida por el cliente.|  
|*Regular*|El atributo representa un atributo normal.|  
|*RelationToParent*|El atributo representa una relación con un primario.|  
|*ReportingDay*|El atributo representa los días de un calendario de informes.|  
|*ReportingDayOfHalfYears*|El atributo representa el ordinal del día en un semestre de un calendario de informes.|  
|*ReportingDayOfMonth*|El atributo representa el ordinal del día en un mes de un calendario de informes.|  
|*ReportingDayOfQuarter*|El atributo representa el ordinal del día en un trimestre de un calendario de informes.|  
|*ReportingDayOfTrimester*|El atributo representa el ordinal del día en un cuatrimestre de un calendario de informes.|  
|*ReportingDayOfWeek*|El atributo representa el ordinal del día en una semana de un calendario de informes.|  
|*ReportingDayOfYear*|El atributo representa el ordinal del día en un año de un calendario de informes.|  
|*ReportingHalfYears*|El atributo representa los semestres de un calendario de informes.|  
|*ReportingHalfYearsOfYear*|El atributo representa el ordinal del semestre en un año de un calendario de informes.|  
|*ReportingMonth*|El atributo representa los meses de un calendario de informes.|  
|*ReportingMonthOfHalfYears*|El atributo representa el ordinal del mes en un semestre de un calendario de informes.|  
|*ReportingMonthOfQuarter*|El atributo representa el ordinal del mes en un trimestre de un calendario de informes.|  
|*ReportingMonthOfTrimester*|El atributo representa el ordinal del mes en un cuatrimestre de un calendario de informes.|  
|*ReportingMonthOfYear*|El atributo representa el ordinal del mes en un año de un calendario de informes.|  
|*ReportingQuarter*|El atributo representa los trimestres de un calendario de informes.|  
|*ReportingQuarterOfHalfYear*|El atributo representa el ordinal del trimestre en un semestre de un calendario de informes.|  
|*ReportingQuarterOfYear*|El atributo representa el ordinal del trimestre en un año de un calendario de informes.|  
|*ReportingTrimester*|El atributo representa los cuatrimestres de un calendario de informes.|  
|*ReportingTrimesterOfYear*|El atributo representa el ordinal del cuatrimestre en un año de un calendario de informes.|  
|*ReportingWeek*|El atributo representa las semanas de un calendario de informes.|  
|*ReportingWeekOfHalfYears*|El atributo representa el ordinal de la semana en un semestre de un calendario de informes.|  
|*ReportingWeekOfMonth*|El atributo representa el ordinal de la semana en un mes de un calendario de informes.|  
|*ReportingWeekOfQuarter*|El atributo representa el ordinal de la semana en un trimestre de un calendario de informes.|  
|*ReportingWeekOfTrimester*|El atributo representa el ordinal de la semana en un cuatrimestre de un calendario de informes.|  
|*ReportingWeekOfYear*|El atributo representa el ordinal de la semana en un año de un calendario de informes.|  
|*ReportingYear*|El atributo representa los años de un calendario de informes.|  
|*Representante*|El atributo representa un representante.|  
|*Escenario*|El atributo representa un escenario.|  
|*Segundos*|El atributo representa los segundos.|  
|*Secuencia*|El atributo representa un atributo de secuencia.|  
|*ShortCaption*|El atributo representa un título corto.|  
|*StateOrProvince*|El atributo representa un estado o provincia.|  
|*TenDayOfHalfYears*|El atributo representa el ordinal de un período de diez días de un semestre.|  
|*TenDayOfQuarter*|El atributo representa el ordinal de un período de diez días de un trimestre.|  
|*TenDayOfTrimester*|El atributo representa el ordinal de un período de diez días de un cuatrimestre.|  
|*TenDayOfYear*|El atributo representa el ordinal de un período de diez días de un año.|  
|*TenDays*|El atributo representa períodos de diez días.|  
|*TenDaysOfMonth*|El atributo representa el ordinal de un período de diez días de un mes.|  
|*Cuatrimestre*|El atributo representa los cuatrimestres.|  
|*TrimesterOfYear*|El atributo representa el ordinal del cuatrimestre de un año.|  
|*UndefinedTime*|El atributo representa un período de tiempo indefinido.|  
|*Utilidad*|El atributo representa una utilidad.|  
|*Versión*|El atributo representa una versión.|  
|*WebHtml*|El atributo representa contenido HTML.|  
|*WebMailAlias*|El atributo representa un alias de correo electrónico.|  
|*WebUrl*|El atributo representa una dirección URL.|  
|*WebXmlOrXsl*|El atributo representa contenido XML o XSL.|  
|*WeekOfHalfYears*|El atributo representa el ordinal de la semana de un semestre.|  
|*WeekOfMonth*|El atributo representa el ordinal de la semana de un mes.|  
|*WeekOfQuarter*|El atributo representa el ordinal de la semana de un trimestre.|  
|*WeekOfTrimester*|El atributo representa el ordinal de la semana de un cuatrimestre.|  
|*WeekOfYear*|El atributo representa el ordinal de la semana de un año.|  
|*Semanas*|El atributo representa las semanas.|  
|*Años*|El atributo representa los años.|  
  
 La enumeración que corresponde a los valores permitidos para **tipo** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.AttributeType>.  
  
 El elemento que corresponde al elemento primario de **tipo** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento Attributes &#40; ASSL &#41;](../../../analysis-services/scripting/collections/attributes-element-assl.md)   
 [Dimension, elemento &#40; ASSL &#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
