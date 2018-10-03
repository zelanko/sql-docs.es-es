---
title: Generar automáticamente valores para el atributo Code (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
ms.assetid: 19b354ee-2906-4cc7-ba2f-32b4543bddcf
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 42887c9126014a1a1bd56217a915539306959275
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48207824"
---
# <a name="automatically-generate-code-attribute-values-master-data-services"></a>Generar automáticamente valores para el atributo Code (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], genere automáticamente valores para el atributo Code de una entidad si desea que se asigne automáticamente un entero cada vez que se cree un nuevo miembro.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   La entidad debe existir. Para obtener más información, consulte [Crear una entidad &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-entity-master-data-services.md).  
  
### <a name="to-automatically-generate-code-values"></a>Para generar automáticamente valores Code  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En el **el Explorador de modelos** página, en la barra de menús, seleccione **administrar** y haga clic en **entidades**.  
  
3.  En la página **Mantenimiento de entidades** , en la lista **Modelo** , seleccione un modelo.  
  
4.  Seleccione la fila para la entidad para la que desea generar códigos.  
  
5.  Haga clic en **Editar entidad seleccionada**.  
  
6.  Active la casilla **Crear automáticamente valores Code** .  
  
7.  En el cuadro **Empezar con** , escriba un número para ir incrementándolo. Si ya existen miembros, el valor Code se establece según el mayor valor existente. Por ejemplo, si el mayor valor Code existente es 299, el valor Code del miembro siguiente se establecerá en 300.  
  
8.  Haga clic en **Guardar entidad**.  
  
## <a name="see-also"></a>Vea también  
 [Creación automática de código &#40;Master Data Services&#41;](../../2014/master-data-services/automatic-code-creation-master-data-services.md)   
 [Generar automáticamente valores de atributo que no sean Code &#40;Master Data Services&#41;](../../2014/master-data-services/automatically-generate-attribute-values-other-than-code-master-data-services.md)  
  
  
