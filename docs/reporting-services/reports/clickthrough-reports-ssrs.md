---
title: Informes Click-through (SSRS) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- clickthrough reports
- customizing clickthrough reports
- clickthrough reports, customizing
ms.assetid: cf2c396e-b0c6-41f9-8c45-ddc8406f7e85
caps.latest.revision: 28
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 55d22d2fd64faef6e913bf226c831546d71665ca
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="clickthrough-reports-ssrs"></a>Informes click-through (SSRS)
  Un informe click-through es aquel que proporciona información detallada sobre los datos incluidos en el informe principal. Un informe click-through se muestra cuando el usuario hace clic en los datos interactivos que aparecen en el informe principal. Estos informes son generados automáticamente por el servidor de informes. El usuario, como diseñador del modelo, determina lo que se ve en los informes click-through estableciendo las propiedades **DefaultDetailAttribute** y **DefaultAggregateAttribute** que se asignan a una entidad del modelo de informe.  
  
> [!NOTE]  
>  Los informes click-through no están disponibles en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md). Si no está seguro de la edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la que trabaja su organización, póngase en contacto con el administrador de la base de datos.  
  
## <a name="using-default-templates"></a>Usar plantillas predeterminadas  
 De manera predeterminada, el servidor de informes genera dos tipos de plantilla click-through para cada entidad: una plantilla de una sola instancia y una plantilla de varias instancias. El elemento sobre el que haga clic determinará la plantilla que se utilizará. Si la persona que lee el informe hace clic en un atributo escalar, se utilizará la plantilla de una sola instancia. Si la persona que lee el informe hace clic en un atributo de agregado, se utilizará la plantilla de varias instancias.  
  
#### <a name="single-instance-templates"></a>Plantillas de una sola instancia  
 Una plantilla de una sola instancia muestra todos los atributos de la entidad de destino y los atributos de agregado predeterminados que se hayan especificado para las entidades relacionadas que tienen un relación de uno a varios desde la entidad de destino. Una plantilla de una sola instancia tiene un aspecto similar al de la siguiente imagen.  
  
 ![Una de varios a 1 informe de Click-through. ] (../../reporting-services/reports/media/manytooneclickthrough.gif "De varios a 1 informe de Click-through.")  
  
#### <a name="multiple-instance-templates"></a>Plantillas de varias instancias  
 Una plantilla de varias instancias muestra solo los atributos de detalle predeterminados de la entidad de destino y todos los atributos de agregado predeterminados que se hayan especificado para las entidades relacionadas que tienen un relación de uno a varios desde la entidad de destino. Una plantilla de varias instancias tiene un aspecto similar al de la siguiente imagen.  
  
 ![Una de varios a 1 informe de Click-through. ] (../../reporting-services/reports/media/onetomanyclickthrough.gif "De varios a 1 informe de Click-through.")  
  
## <a name="customizing-clickthrough-reports"></a>personalizar informes click-through  
 En lugar de usar las plantillas predeterminadas que genera el servidor de informes, puede crear un informe en el Generador de informes y utilizarlo como informe click-through personalizado. A continuación, puede vincular el informe al modelo como un informe detallado en el Administrador de informes.  
  
 Para convertir un informe del Generador de informes en un informe click-through, debe seleccionar la opción **Permitir que los usuarios obtengan detalles de este informe a partir de otros informes** en el cuadro de diálogo **Propiedades** del Generador de informes. Una vez que esta opción se ha seleccionado, se agregará un parámetro drill-through al informe y éste ya no podrá ejecutarse directamente en el Generador de informes. El servidor de informes calcula automáticamente el parámetro drill-through cuando la persona que lee el informe hace clic en un elemento del informe del Generador de informes.  
  
> [!IMPORTANT]  
>  La entidad principal o base utilizada en el informe debe ser la misma a la que vincule el informe.  
  
## <a name="see-also"></a>Vea también  
 [Vincular un informe a un modelo como informe click-through](http://msdn.microsoft.com/library/3af42de3-67ef-41c2-bc8a-7045baec6f63)  
  
  

