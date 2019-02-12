---
title: Informes click-through (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- clickthrough reports
- customizing clickthrough reports
- clickthrough reports, customizing
ms.assetid: cf2c396e-b0c6-41f9-8c45-ddc8406f7e85
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: caf23eb7e7d0e06a9e79dbaa6b9a0120725a4b10
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56031056"
---
# <a name="clickthrough-reports-ssrs"></a>Informes click-through (SSRS)
  Un informe click-through es aquel que proporciona información detallada sobre los datos incluidos en el informe principal. Un informe click-through se muestra cuando el usuario hace clic en los datos interactivos que aparecen en el informe principal. Estos informes son generados automáticamente por el servidor de informes. El usuario, como diseñador del modelo, determina lo que se ve en los informes click-through estableciendo las propiedades `DefaultDetailAttribute` y `DefaultAggregateAttribute` que se asignan a una entidad del modelo de informe.  
  
> [!NOTE]
>  Los informes click-through no están disponibles en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vea [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md). Si no está seguro de la edición de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con la que trabaja su organización, póngase en contacto con el administrador de la base de datos.  
  
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
  
  
