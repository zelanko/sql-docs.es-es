---
title: Informes click-through (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- clickthrough reports
- customizing clickthrough reports
- clickthrough reports, customizing
ms.assetid: cf2c396e-b0c6-41f9-8c45-ddc8406f7e85
caps.latest.revision: 28
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 2f8c96a114557bcef8252f2c21b70c9a50dbfb94
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37216655"
---
# <a name="clickthrough-reports-ssrs"></a>Informes click-through (SSRS)
  Un informe click-through es aquel que proporciona información detallada sobre los datos incluidos en el informe principal. Un informe click-through se muestra cuando el usuario hace clic en los datos interactivos que aparecen en el informe principal. Estos informes son generados automáticamente por el servidor de informes. Usted, como el Diseñador de modelos, determina lo que se muestra en los informes Click-through estableciendo el `DefaultDetailAttribute` y `DefaultAggregateAttribute` propiedades que se asignan a una entidad del modelo de informe.  
  
> [!NOTE]  
>  Informes Click-through no están disponibles en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vea [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md). Si no está seguro de la edición de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con la que trabaja su organización, póngase en contacto con el administrador de la base de datos.  
  
## <a name="using-default-templates"></a>Usar plantillas predeterminadas  
 De manera predeterminada, el servidor de informes genera dos tipos de plantilla click-through para cada entidad: una plantilla de una sola instancia y una plantilla de varias instancias. El elemento sobre el que haga clic determinará la plantilla que se utilizará. Si la persona que lee el informe hace clic en un atributo escalar, se utilizará la plantilla de una sola instancia. Si la persona que lee el informe hace clic en un atributo de agregado, se utilizará la plantilla de varias instancias.  
  
#### <a name="single-instance-templates"></a>Plantillas de una sola instancia  
 Una plantilla de una sola instancia muestra todos los atributos de la entidad de destino y los atributos de agregado predeterminados que se hayan especificado para las entidades relacionadas que tienen un relación de uno a varios desde la entidad de destino. Una plantilla de una sola instancia tiene un aspecto similar al de la siguiente imagen.  
  
 ![Informe click-through varios a uno.](../media/manytooneclickthrough.gif "Informe click-through varios a uno.")  
  
#### <a name="multiple-instance-templates"></a>Plantillas de varias instancias  
 Una plantilla de varias instancias muestra solo los atributos de detalle predeterminados de la entidad de destino y todos los atributos de agregado predeterminados que se hayan especificado para las entidades relacionadas que tienen un relación de uno a varios desde la entidad de destino. Una plantilla de varias instancias tiene un aspecto similar al de la siguiente imagen.  
  
 ![Informe click-through varios a uno.](../media/onetomanyclickthrough.gif "Informe click-through varios a uno.")  
  
## <a name="customizing-clickthrough-reports"></a>personalizar informes click-through  
 En lugar de usar las plantillas predeterminadas que genera el servidor de informes, puede crear un informe en el Generador de informes y utilizarlo como informe click-through personalizado. A continuación, puede vincular el informe al modelo como un informe detallado en el Administrador de informes.  
  
 Para convertir un informe del Generador de informes en un informe click-through, debe seleccionar la opción **Permitir que los usuarios obtengan detalles de este informe a partir de otros informes** en el cuadro de diálogo **Propiedades** del Generador de informes. Una vez que esta opción se ha seleccionado, se agregará un parámetro drill-through al informe y éste ya no podrá ejecutarse directamente en el Generador de informes. El servidor de informes calcula automáticamente el parámetro drill-through cuando la persona que lee el informe hace clic en un elemento del informe del Generador de informes.  
  
> [!IMPORTANT]  
>  La entidad principal o base utilizada en el informe debe ser la misma a la que vincule el informe.  
  
## <a name="see-also"></a>Vea también  
 [Vincular un informe a un modelo como informe click-through](../link-a-report-to-a-model-as-a-clickthrough-report.md)  
  
  
