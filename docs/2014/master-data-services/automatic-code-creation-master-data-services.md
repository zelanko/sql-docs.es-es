---
title: Creación automática de código (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
ms.assetid: 9adbd5e1-f28c-4fb5-afa7-082de2831f3e
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: b981d40631de5185f2e62c11be8f4c8b8eec880b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48214635"
---
# <a name="automatic-code-creation-master-data-services"></a>Creación automática de código (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], los valores numéricos pueden generarse automáticamente para el atributo Code o para cualquier otro atributo numérico. Cuando se generan códigos automáticamente, no se impide introducir otros valores para los códigos; en su lugar, se establece automáticamente un valor inicial.  
  
## <a name="generating-code-values"></a>Generar valores de código  
 Los administradores pueden configurar valores generados automáticamente para el atributo Code si modifican las propiedades asociadas de la entidad. Pueden especificar un valor inicial y cada valor subsiguiente aumentará en uno.  
  
 Al escribir valores de código en MDS, bien en una de las herramientas o mediante el proceso de almacenamiento provisional, puede dejar en blanco el valor de código, que se generará automáticamente. O bien, puede especificar el valor de código que desee.  
  
## <a name="generating-other-attribute-values"></a>Generar otros valores de atributo  
 Los administradores pueden generar automáticamente valores de atributos distintos de Code si crean reglas de negocios. Pueden especificar un valor inicial y especificar el número en que se incrementa cada valor siguiente.  
  
 Al escribir valores de atributo en MDS, ya sea en una de las herramientas o mediante el proceso de almacenamiento provisional, puede dejar en blanco el valor de atributo. Cuando se aplican reglas de negocios, los valores se incrementan en función del mayor valor existente. Por ejemplo, si la regla es 'establecer como atributo predeterminado para un valor generado que comienza en 1 y se incrementa en 4' y el valor actual más grande del atributo es 700, el valor del siguiente miembro que se agregue será 704.  
  
## <a name="deleting-automatically-generated-values"></a>Eliminar valores generados automáticamente  
 Una vez que un administrador ha habilitado los valores generados automáticamente para el atributo Code, los usuarios pueden eliminar accidentalmente un miembro que tenía un valor de código que desean usar. Se mostrará el mensaje de error 'El código de miembro ya lo usa un miembro que se eliminó'. Hay dos posibles soluciones:  
  
-   En el área funcional **Administración de versiones** , un administrador puede invertir las transacción que se produjo cuando se eliminó el miembro. Sin embargo, esto significa que todos los atributos anteriores y la pertenencia del miembro a jerarquías y colecciones se restauran. Para obtener más información, consulte [invertir una transacción &#40;Master Data Services&#41;](reverse-a-transaction-master-data-services.md).  
  
-   Un administrador puede utilizar el proceso de almacenamiento provisional para eliminar permanentemente el miembro. Para obtener más información, consulte [desactivar o eliminar miembros usando el proceso de ensayo &#40;Master Data Services&#41;](add-update-and-delete-data-master-data-services.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Generar automáticamente valores para el atributo Code.|[Generar automáticamente valores de atributo de código &#40;Master Data Services&#41;](../../2014/master-data-services/automatically-generate-code-attribute-values-master-data-services.md)|  
|Generar automáticamente valores para otros atributos.|[Generar automáticamente valores de atributo que no sean Code &#40;Master Data Services&#41;](../../2014/master-data-services/automatically-generate-attribute-values-other-than-code-master-data-services.md)|  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   [Introducción a Master Data Services](master-data-services-overview-mds.md)  
  
-   [Las reglas de negocios &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
-   [Entidades &#40;Master Data Services&#41;](../../2014/master-data-services/entities-master-data-services.md)  
  
  
