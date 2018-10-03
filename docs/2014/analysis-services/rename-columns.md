---
title: 'Lección 3: Cambiar el nombre de columnas | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 5fc8ba1a-2b30-4775-9b3b-c09dee711b3e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0037d13dd84f3db8243252717fad1d59fd380bd9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48152965"
---
# <a name="lesson-3-rename-columns"></a>Lección 3: Cambiar el nombre de las columnas
  En esta lección, cambiará el nombre de muchas de las columnas de cada tabla que ha importado. El cambio de nombre permite navegar de forma más sencilla por el diseñador de modelos y facilita la selección de campos de los usuarios en una aplicación cliente. Para obtener más información, consulte [Cambiar el nombre de una tabla o una columna &#40;SSAS tabular&#41;](tabular-models/rename-a-table-or-column-ssas-tabular.md).  
  
> [!IMPORTANT]  
>  El cambio de nombre de las columnas no es necesario para completar este tutorial; sin embargo, las lecciones restantes, especialmente en las que hay que crear relaciones, así como crear columnas calculadas y medidas mediante fórmulas DAX, hacen referencia a los nombres descriptivos que se indican en esta lección. Si decide no cambiar el nombre de las columnas, tendrá que editar las fórmulas DAX en las lecciones 5, 6 y 7 para utilizar los nombres de las columnas de origen originales proporcionados en esta lección.  
  
 Tiempo estimado para completar esta lección: **20 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
 Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 2: Agregar datos](lesson-2-add-data.md).  
  
## <a name="rename-columns"></a>Cambiar el nombre de las columnas  
  
#### <a name="to-rename-columns"></a>Para cambiar el nombre de las columnas  
  
1.  En el diseñador de modelos, haga clic en la pestaña de la tabla **Customer** .  
  
     Al hacer clic en una pestaña, la tabla se activa en la ventana del diseñador de modelos.  
  
2.  Haga doble clic en el **CustomerKey** columna nombre, a continuación, escriba `Customer  Id`, y, a continuación, presione ENTRAR.  
  
    > [!TIP]  
    >  También puede cambiar el nombre de una columna en la propiedad **Nombre de columna** en la ventana **Propiedades** de la columna o en la Vista de diagrama.  
  
3.  Cambie el nombre de las columnas restantes de la tabla **Customer** , así como el de las columnas de las demás tablas, y sustituya el nombre de origen por el nombre descriptivo:  
  
     **Tabla de clientes**  
  
    |Nombre de origen|Nombre descriptivo|  
    |-----------------|-------------------|  
    |GeographyKey|Geography Id|  
    |CustomerAlternateKey|Id. alternativo del cliente|  
    |FirstName|Nombre|  
    |MiddleName|Segundo nombre|  
    |LastName|Apellidos|  
    |NameStyle|Estilo del nombre|  
    |BirthDate|Birth Date|  
    |MaritalStatus|Marital Status|  
    |EmailAddress|Email Address|  
    |YearlyIncome|Yearly Income|  
    |TotalChildren|Total Children|  
    |NumberChildrenAtHome|Hijos a su cuidado|  
    |EnglishEducation|Education|  
    |EnglishOccupation|Occupation|  
    |HouseOwnerFlag|Propietario de una vivienda|  
    |NumberCarsOwned|Número de vehículos en propiedad|  
    |AddressLine1|Línea de dirección 1|  
    |AddressLine2|Línea de dirección 2|  
    |Teléfono|Número de teléfono|  
    |DateFirstPurchase|Fecha de la primera compra|  
    |CommuteDistance|Commute Distance|  
  
     **Date**  
  
    |Nombre de origen|Nombre descriptivo|  
    |-----------------|-------------------|  
    |FullDateAlternateKey|date|  
    |DayNumberOfWeek|Día de la semana|  
    |EnglishDayNameOfWeek|Nombre del día|  
    |DayNumberOfMonth|Día del mes|  
    |DayNumberOfYear|Día del año|  
    |WeekNumberOfYear|Número de semana del año|  
    |EnglishMonthName|Nombre del mes|  
    |MonthNumberOfYear|Month|  
    |CalendarQuarter|Trimestre del calendario|  
    |CalendarYear|Año del calendario|  
    |CalendarSemester|Semestre del calendario|  
    |FiscalQuarter|Trimestre fiscal|  
    |FiscalYear|Año fiscal|  
    |FiscalSemester|Semestre fiscal|  
  
     **Geography**  
  
    |Nombre de origen|Nombre descriptivo|  
    |-----------------|-------------------|  
    |GeographyKey|Id. de geografía|  
    |StateProvinceCode|Código de estado o provincia|  
    |StateProvinceName|Nombre de estado o provincia|  
    |CountryRegionCode|Código de país o región|  
    |SpanishCountryRegionName|Nombre de país o región|  
    |PostalCode|Código postal|  
    |SalesTerritoryKey|Sales Territory Id|  
  
     **Product**  
  
    |Nombre de origen|Nombre descriptivo|  
    |-----------------|-------------------|  
    |ProductKey|Product Id|  
    |ProductAlternateKey|Id. alternativo del producto|  
    |ProductSubcategoryKey|Id. de subcategoría del producto|  
    |WeightUnitMeasureCode|Código de unidad de peso|  
    |SizeUnitMeasureCode|Código de unidad de tamaño|  
    |EnglishProductName|Nombre del producto|  
    |StandardCost|Standard Cost|  
    |FinishedGoodsFlag|Es producto final|  
    |SafetyStockLevel|Safety Stock Level|  
    |ReorderPoint|Reorder Point|  
    |ListPrice|List Price|  
    |SizeRange|Size Range|  
    |DaysToManufacture|Días hasta fabricación|  
    |ProductLine|Línea de productos|  
    |Dealer Price|Dealer Price|  
    |ModelName|Nombre del modelo|  
    |LargePhoto|Foto grande|  
    |EnglishDescription|Descripción|  
    |StartDate|Fecha de inicio del producto|  
    |EndDate|Fecha de finalización del producto|  
    |Estado|Estado del producto|  
  
     **Categoría de producto**  
  
    |Nombre de origen|Nombre descriptivo|  
    |-----------------|-------------------|  
    |ProductCategoryKey|Id. de categoría del producto|  
    |ProductCategoryAlternateKey|Id. alternativo de categoría del producto|  
    |EnglishProductCategoryName|Nombre de categoría del producto|  
  
     **Subcategoría de producto**  
  
    |Nombre de origen|Nombre descriptivo|  
    |-----------------|-------------------|  
    |ProductSubcategoryKey|Id. de subcategoría del producto|  
    |ProductSubcategoryAlternateKey|Id. alternativo de subcategoría del producto|  
    |EnglishProductSubcategoryName|Nombre de subcategoría del producto|  
    |ProductCategoryKey|Id. de categoría del producto|  
  
     **Internet Sales**  
  
    |Nombre de origen|Nombre descriptivo|  
    |-----------------|-------------------|  
    |ProductKey|Id. de producto|  
    |CustomerKey|Id. de cliente|  
    |PromotionKey|Id. de promoción|  
    |CurrencyKey|Id. de moneda|  
    |SalesTerritoryKey|Sales Territory Id|  
    |SalesOrderNumber|Número de pedido de ventas|  
    |SalesOrderLineNumber|Número de líneas del pedido de venta|  
    |RevisionNumber|Revision Number|  
    |OrderQuantity|Cantidad del pedido|  
    |UnitPrice|Unit Price|  
    |ExtendedAmount|Extended Amount|  
    |UnitPriceDiscountPct|Porcentaje de descuento del precio por unidad|  
    |DiscountAmount|Discount Amount|  
    |ProductStandardCost|Product Standard Cost|  
    |TotalProductCost|Total Product Cost|  
    |SalesAmount|Sales Amount|  
    |TaxAmt|Tax Amt|  
    |CarrierTrackingNumber|Número de seguimiento del transportista|  
    |CustomerPONumber|Número de orden de compra del cliente|  
    |OrderDate|Fecha de pedido|  
    |DueDate|Fecha de vencimiento|  
    |ShipDate|Fecha de envío|  
  
## <a name="next-step"></a>Paso siguiente  
 Para continuar este tutorial, vaya a la lección siguiente: [Lección 4: Marcar como tabla de fechas](lesson-3-mark-as-date-table.md).  
  
  
