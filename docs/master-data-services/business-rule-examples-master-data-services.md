---
title: Ejemplos de reglas de negocios (Master Data Services) | Microsoft Docs
ms.custom: 
ms.date: 01/05/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3974b9be-4b7c-4a37-ab26-1a36ef455744
caps.latest.revision: "21"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3bb7af051f64737458f34655aac731c85ab34701
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="business-rule-examples-master-data-services"></a>Ejemplos de reglas de negocios (Master Data Services)
En este artículo se muestran ejemplos de reglas de negocios para [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]. Encontrará estos ejemplos en los modelos de ejemplo que se incluyen con la instalación de [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)].   
  
Para obtener instrucciones sobre cómo implementar los modelos de ejemplo, vea [Instalación y configuración de Master Data Services](../master-data-services/master-data-services-installation-and-configuration.md).  
  
  
## <a name="business-rule-examples"></a>Ejemplos de reglas de negocios  
Modelo de ejemplo |Entidad  |Nombre de la regla de negocio| Description  
---------|---------|---------|-----------|  
Customer    | Customer   | Person pmt terms| Especifica las condiciones de pago predeterminadas para los clientes.          
En la siguiente regla de negocio, si el valor del atributo CustomerType cumple la `is equal` [rule condition](../master-data-services/business-rule-conditions-master-data-services.md), then the `defaults to` [rule action](../master-data-services/business-rule-conditions-master-data-services.md) is applied to the PaymentTerms attribute. De lo contrario, no se realiza ninguna acción.  
```  
If  
    CustomerType is equal to 2  
Then  
    PaymentTerms defaults to CASH  
Else  
    None      
```  
  
**--------------------------------------------------**  
  
Modelo de ejemplo  |Entidad  |Nombre de la regla de negocio|Description    
---------|---------|---------|---------------  
Customer     | Customer    | Org pmt terms | Especifica las condiciones de pago predeterminadas para las organizaciones.         
En la siguiente regla de negocio, si el valor del atributo CustomerType cumple la `is equal` [rule condition](../master-data-services/business-rule-conditions-master-data-services.md), then the `defaults to` [rule action](../master-data-services/business-rule-actions-master-data-services.md) is applied to the PaymentTerms attribute. De lo contrario, no se realiza ninguna acción.  
```  
If  
    CustomerType is equal to 1  
Then  
    PaymentTerms defaults to 210Net30  
Else  
    None  
```  
  
**--------------------------------------------------**  
  
  
Modelo de ejemplo  |Entidad  |Nombre de la regla de negocio| Description    
---------|---------|---------|-----------  
Product     |  Product       | DaysToManufacture |Especifica el intervalo de días de fabricación para la fabricación interna.          
En la siguiente regla de negocio, si el valor del atributo InHouseManufacture cumple la `is equal` [rule condition](../master-data-services/business-rule-conditions-master-data-services.md), then the `must be between` [rule action](../master-data-services/business-rule-actions-master-data-services.md) is applied to the DaysToManufacture attribute. De lo contrario, no se realiza ninguna acción.  
```  
If  
    InHouseManufacture is equal to Y  
Then  
    DaysToManufacture must be between 1 and 10  
Else  
    None  
```  
  
**--------------------------------------------------**  
  
  
Modelo de ejemplo  |Entidad  |Nombre de la regla de negocio|Description    
---------|---------|---------|-------------  
Product     |Product         |Required fields| Especifica los atributos necesarios para los miembros de la entidad de producto.           
En la siguiente regla de negocio, en todas las condiciones se realiza la `is required` [validation action](../master-data-services/business-rule-actions-master-data-services.md) is taken for the specified attributes. Los valores de atributo no pueden ser NULL ni estar en blanco.  
```  
If  
    None  
Then  
    Name is required  
    ProductSubCategory is required  
    Color is required  
    StandardCost is required  
    SafetyStockLevel is required  
    ReorderPoint is required  
    InHouseManufacture is required  
    SellStartDate is required  
    FinishedGoodIndicator is required  
    ProductLine is required  
Else  
    None  
```  
  
**--------------------------------------------------**  
  
  
Modelo de ejemplo  |Entidad  |Nombre de la regla de negocio|Description    
---------|---------|---------|-----------  
Product     | Product        |  Std Cost| Requiere que el costo estándar sea mayor que 0.        
En la siguiente regla de negocio, en todas las condiciones se aplica la `must be greater than` [rule action](../master-data-services/business-rule-actions-master-data-services.md) is applied to the StandardCost attribute of products.  
```  
If  
    None  
Then  
    StandardCost must be greater than 0  
Else  
    None  
```  
  
**--------------------------------------------------**  
  
  
Modelo de ejemplo  |Entidad  |Nombre de la regla de negocio|Description    
---------|---------|---------|------------  
Product     | Product        | FG MSRP Cost|Especifica que, si el producto es un producto terminado, el MSRP (precio minorista sugerido por el fabricante) y los costos del distribuidor deben ser mayores que 0.           
  
En la siguiente regla de negocio, si el valor del atributo FinishedGoodIndicator cumple la `is equal` [rule condition](../master-data-services/business-rule-conditions-master-data-services.md), the `must be greater than` [rule action](../master-data-services/business-rule-actions-master-data-services.md) is applied to the MSRP and DealerCost attributes.  
```  
If  
    FinishedGoodIndicator is equal to Y  
Then  
    MSRP must be greater than 0  
    DealerCost must be greater than 0  
Else  
    None  
```  
  
**--------------------------------------------------**  
  
  
Modelo de ejemplo  |Entidad  |Nombre de la regla de negocio|Description    
---------|---------|---------|------------  
Product     | Product        |  Default Name| Especifica el nombre predeterminado del producto según los valores de los atributos Color y Class. Cuando el valor del atributo Color no es YLO y el atributo Class no es NA, el nombre predeterminado es Yellow NA.         
En la siguiente regla de negocio, si los atributos Color y Class no cumplen la condición de regla `is equal` , la `defaults to` [rule action](../master-data-services/business-rule-actions-master-data-services.md) is applied to the Name attribute.  
```  
If  
    (Color is equal to YLO AND Class is equal to NA) is not true  
Then  
    Name defaults to Yellow NA  
Else  
    Name defaults to Other  
```  
  
**--------------------------------------------------**  
  
  
**Para ver ejemplos de reglas de negocios en los modelos de ejemplo**  
1. Vaya al sitio web de [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] que ha configurado después de instalar MDS y haga clic en el cuadro **Administración del sistema** .   
Para obtener instrucciones sobre cómo configurar el sitio web, vea [Instalación y configuración de Master Data Services](../master-data-services/master-data-services-installation-and-configuration.md).  
2. Haga clic en el modelo de ejemplo que contiene la regla de negocio, como se muestra en las tablas anteriores, y, después, haga clic en **Entidades**.  
3. Haga clic en la entidad a la que se aplica la regla, como se muestra en las tablas anteriores, y, luego, haga clic en **Reglas de negocios**.  
4. Haga clic en el nombre de la regla de negocio que quiera ver. La interfaz de usuario se expande y muestra las instrucciones **If**, **Then** y **Else** .  
  
## <a name="did-this-article-help-you-were-listening"></a>¿Le ayudó este artículo? Le escuchamos   
¿Qué información está buscando? ¿La encontró? Escuchamos sus comentarios para mejorar el contenido. Envíe sus comentarios a [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com).   
  
  
  
  

