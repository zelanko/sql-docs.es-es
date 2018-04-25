---
title: Creación automática de código (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9adbd5e1-f28c-4fb5-afa7-082de2831f3e
caps.latest.revision: 8
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 82b145eb8a947c9320b4c4cb261d3a83e623d094
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="automatic-code-creation-master-data-services"></a>Creación automática de código (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], los valores numéricos pueden generarse automáticamente para el atributo Code o para cualquier otro atributo numérico. Cuando se generan códigos automáticamente, no se impide introducir otros valores para los códigos; en su lugar, se establece automáticamente un valor inicial.  
  
## <a name="generating-code-values"></a>Generar valores de código  
 Los administradores pueden configurar valores generados automáticamente para el atributo Code si modifican las propiedades asociadas de la entidad. Pueden especificar un valor inicial y cada valor subsiguiente aumentará en uno.  
  
 Al escribir valores de código en MDS, bien en una de las herramientas o mediante el proceso de almacenamiento provisional, puede dejar en blanco el valor de código, que se generará automáticamente. O bien, puede especificar el valor de código que desee.  
  
## <a name="generating-other-attribute-values"></a>Generar otros valores de atributo  
 Los administradores pueden generar automáticamente valores de atributos distintos de Code si crean reglas de negocios. Pueden especificar un valor inicial y especificar el número en que se incrementa cada valor siguiente.  
  
 Al escribir valores de atributo en MDS, ya sea en una de las herramientas o mediante el proceso de almacenamiento provisional, puede dejar en blanco el valor de atributo. Cuando se aplican reglas de negocios, los valores se incrementan en función del mayor valor existente. Por ejemplo, si la regla es 'establecer como atributo predeterminado para un valor generado que comienza en 1 y se incrementa en 4' y el valor actual más grande del atributo es 700, el valor del siguiente miembro que se agregue será 704.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Generar automáticamente valores para el atributo Code.|[Generar automáticamente valores para el atributo Code &#40;Master Data Services&#41;](../master-data-services/automatically-generate-code-attribute-values-master-data-services.md)|  
|Generar automáticamente valores para otros atributos.|[Generar automáticamente valores de atributo que no sean Code &#40;Master Data Services&#41;](../master-data-services/automatically-generate-attribute-values-other-than-code-master-data-services.md)|  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   [Introducción a Master Data Services &#40;MDS&#41;](../master-data-services/master-data-services-overview-mds.md)  
  
-   [Reglas de negocios &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
-   [Entidades &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)  
  
  
