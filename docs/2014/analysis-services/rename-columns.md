---
title: 'Lección 3: cambiar el nombre de las columnas | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5fc8ba1a-2b30-4775-9b3b-c09dee711b3e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 80d9cae6deae4059327084f531f6a6d958a39ec6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66070318"
---
# <a name="lesson-3-rename-columns"></a>Lección 3: Cambiar el nombre de las columnas
  En esta lección, cambiará el nombre de muchas de las columnas de cada tabla que ha importado. El cambio de nombre permite navegar de forma más sencilla por el diseñador de modelos y facilita la selección de campos de los usuarios en una aplicación cliente. Para obtener más información, consulte [Cambiar el nombre de una tabla o una columna &#40;SSAS tabular&#41;](tabular-models/rename-a-table-or-column-ssas-tabular.md).  
  
> [!IMPORTANT]  
>  El cambio de nombre de las columnas no es necesario para completar este tutorial; sin embargo, las lecciones restantes, especialmente en las que hay que crear relaciones, así como crear columnas calculadas y medidas mediante fórmulas DAX, hacen referencia a los nombres descriptivos que se indican en esta lección. Si decide no cambiar el nombre de las columnas, tendrá que editar las fórmulas DAX en las lecciones 5, 6 y 7 para utilizar los nombres de las columnas de origen originales proporcionados en esta lección.  
  
 Tiempo estimado para completar esta lección: **20 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
 Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 2: Agregar datos](lesson-2-add-data.md).  
  
## <a name="rename-columns"></a>Cambiar el nombre de las columnas  
  
#### <a name="to-rename-columns"></a>Para cambiar el nombre de las columnas  
  
1.  En el diseñador de modelos, haga clic en la pestaña de la tabla **Customer** .  
  
     Al hacer clic en una pestaña, la tabla se activa en la ventana del diseñador de modelos.  
  
2.  Haga doble clic **CustomerKey** en el nombre de la columna `Customer  Id`CustomerKey, escriba y, a continuación, presione Entrar.  
  
    > [!TIP]  
    >  También puede cambiar el nombre de una columna en la propiedad **nombre de columna** en la ventana **propiedades** de la columna o en la vista de diagrama.  
  
3.  Cambie el nombre de las columnas restantes de la tabla **Customer** , así como el de las columnas de las demás tablas, y sustituya el nombre de origen por el nombre descriptivo:  
  
     **Tabla Customer**  
  
    |Nombre de origen|Nombre descriptivo|  
    |-----------------|-------------------|  
    |GeographyKey|Geography Id|  
    |CustomerAlternateKey|Id. alternativo del cliente|  
    |Nombre|Nombre|  
    |MiddleName|Segundo nombre|  
    |Apellidos|Apellido|  
    |NameStyle|Estilo del nombre|  
    |BirthDate|Birth Date|  
    |MaritalStatus|Marital Status|  
    |EmailAddress|Dirección de correo electrónico|  
    |YearlyIncome|Yearly Income|  
    |TotalChildren|Total Children|  
    |NumberChildrenAtHome|Hijos a su cuidado|  
    |EnglishEducation|Educación|  
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
    |FullDateAlternateKey|Fecha|  
    |DayNumberOfWeek|Día de la semana|  
    |EnglishDayNameOfWeek|Nombre del día|  
    |DayNumberOfMonth|Día del mes|  
    |DayNumberOfYear|Día del año|  
    |WeekNumberOfYear|Número de semana del año|  
    |EnglishMonthName|Nombre del mes|  
    |MonthNumberOfYear|Mes|  
    |CalendarQuarter|Trimestre del calendario|  
    |CalendarYear|Año del calendario|  
    |CalendarSemester|Semestre del calendario|  
    |FiscalQuarter|Trimestre fiscal|  
    |FiscalYear|Año fiscal|  
    |FiscalSemester|Semestre fiscal|  
  
     **Geografía**  
  
    |Nombre de origen|Nombre descriptivo|  
    |-----------------|-------------------|  
    |GeographyKey|Geography Id|  
    |StateProvinceCode|Código de estado o provincia|  
    |StateProvinceName|Nombre de estado o provincia|  
    |CountryRegionCode|Código de país o región|  
    |SpanishCountryRegionName|Nombre de país o región|  
    |PostalCode|Código postal|  
    |SalesTerritoryKey|Sales Territory Id|  
  
     **Manuales**  
  
    |Nombre de origen|Nombre descriptivo|  
    |-----------------|-------------------|  
    |ProductKey|Product Id|  
    |ProductAlternateKey|Product Alternate Id|  
    |ProductSubcategoryKey|Id. de subcategoría del producto|  
    |WeightUnitMeasureCode|Código de unidad de peso|  
    |SizeUnitMeasureCode|Código de unidad de tamaño|  
    |EnglishProductName|Nombre de producto|  
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
  
     **Categoría de productos**  
  
    |Nombre de origen|Nombre descriptivo|  
    |-----------------|-------------------|  
    |ProductCategoryKey|Id. de categoría del producto|  
    |ProductCategoryAlternateKey|Id. alternativo de categoría del producto|  
    |EnglishProductCategoryName|Nombre de categoría del producto|  
  
     **Product Subcategory**  
  
    |Nombre de origen|Nombre descriptivo|  
    |-----------------|-------------------|  
    |ProductSubcategoryKey|Id. de subcategoría del producto|  
    |ProductSubcategoryAlternateKey|Id. alternativo de subcategoría del producto|  
    |EnglishProductSubcategoryName|Nombre de subcategoría del producto|  
    |ProductCategoryKey|Id. de categoría del producto|  
  
     **Internet Sales**  
  
    |Nombre de origen|Nombre descriptivo|  
    |-----------------|-------------------|  
    |ProductKey|Product Id|  
    |CustomerKey|Customer Id|  
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
    |OrderDate|Order Date|  
    |DueDate|Due Date|  
    |ShipDate|Ship Date|  
  
## <a name="next-step"></a>siguiente paso  
 Para continuar este tutorial, vaya a la lección siguiente: [Lección 4: Marcar como tabla de fechas](lesson-3-mark-as-date-table.md).  
  
  
