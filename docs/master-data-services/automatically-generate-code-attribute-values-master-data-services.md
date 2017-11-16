---
title: "Generar automáticamente valores para el atributo Code (Master Data Services) | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 19b354ee-2906-4cc7-ba2f-32b4543bddcf
caps.latest.revision: "5"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f75fbf0f8ab630615d52ae217566d6b6a8790520
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="automatically-generate-code-attribute-values-master-data-services"></a>Generar automáticamente valores para el atributo Code (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], genere automáticamente valores para el atributo Code de una entidad si desea que se asigne automáticamente un entero cada vez que se cree un nuevo miembro.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   La entidad debe existir. Para obtener más información, consulte [Crear una entidad &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md).  
  
### <a name="to-automatically-generate-code-values"></a>Para generar automáticamente valores Code  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En la página **Administrar modelo** , seleccione la fila correspondiente al modelo que contiene la entidad que desea editar y luego haga clic en **Entidades**.  
  
3.  En la página **Administrar entidad** , seleccione la fila correspondiente a la entidad para la que quiere generar códigos y luego haga clic en **Editar**.  
  
4.  Active la casilla **Crear automáticamente valores Code** .  
  
5.  En el cuadro **Empezar con** , escriba un número para ir incrementándolo. Si ya existen miembros, el valor Code se establece según el mayor valor existente. Por ejemplo, si el mayor valor Code existente es 299, el valor Code del miembro siguiente se establecerá en 300.  
  
6.  Haga clic en **Guardar**.  
  
## <a name="see-also"></a>Vea también  
 [Creación automática de código &#40;Master Data Services&#41;](../master-data-services/automatic-code-creation-master-data-services.md)   
 [Generar automáticamente valores de atributo que no sean Code &#40;Master Data Services&#41;](../master-data-services/automatically-generate-attribute-values-other-than-code-master-data-services.md)  
  
  
