---
title: Agregar varias condiciones a una regla de negocios (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- business rules [Master Data Services], multiple conditions
ms.assetid: 5f0f6958-6cf2-444b-bdcd-05b887637a0b
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: e5ac7bab7712a268e3fe8fd37f1a5ae799ef55dc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196267"
---
# <a name="add-multiple-conditions-to-a-business-rule-master-data-services"></a>Agregar varias condiciones a una regla de negocios (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], agregue varias condiciones **AND** u **OR** a una regla de negocio cuando quiera una regla más compleja.  
  
> [!NOTE]  
>  Si crea una regla de negocio que usa el operador **OR** , considere crear una regla distinta para cada instrucción condicional que se pueda evaluar de forma independiente. A continuación, puede excluir las reglas según sea necesario, proporcionando más flexibilidad y facilitando la solución de problemas.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   Una regla de negocios debe existir. Para obtener más información, consulte [Crear y publicar una regla de negocios &#40;Master Data Services&#41;](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md).  
  
### <a name="to-add-multiple-conditions-to-a-business-rule"></a>Para agregar varias condiciones a una regla de negocios  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En la barra de menús, seleccione **Administrar** y haga clic en **Reglas de negocios**.  
  
3.  En la página **Mantenimiento de reglas de negocios** , en la lista **Modelo** , seleccione un modelo.  
  
4.  En la lista **Entidad** , seleccione una entidad.  
  
5.  Desde el **tipo de miembro** , seleccione un tipo de miembro.  
  
6.  En la lista **Atributo** , seleccione un atributo o deje el valor predeterminado de **Todos**.  
  
7.  Haga clic en la fila de la regla de negocios que desea modificar.  
  
8.  Haga clic en **Editar regla de negocios seleccionada**.  
  
9. En el **componentes** panel, expanda el **operadores lógicos** nodo.  
  
10. Haga clic en **AND** o **OR** y arrástrelo hasta el **IF** del panel **AND** etiqueta.  
  
11. En el panel **Componentes** , expanda el nodo **Condiciones** .  
  
12. Haga clic en una condición y arrástrela hasta **IF** panel, a la **AND** o **OR** etiqueta desde el paso 10.  
  
13. En el **atributos** panel, haga clic en un atributo y arrástrelo hasta el **Editar condición** del panel **Seleccionar atributo** etiqueta.  
  
14. En el **Editar condición** panel, complete los campos obligatorios.  
  
15. En el panel **Editar acción** , haga clic en **Guardar elemento**.  
  
16. Opcionalmente, para agregar más condiciones, desde el **componentes** , arrastre **AND** o **OR** a cualquier **AND** o **OR**en la **IF** panel. A continuación, siga los pasos 13-15.  
  
    > [!TIP]  
    >  Para eliminar una condición, haga clic en el nombre de la condición y en la **Editar condición** panel, haga clic en **eliminar el elemento**.  
  
## <a name="see-also"></a>Vea también  
 [Las reglas de negocios &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)   
 [Cambiar el nombre de una regla de negocios &#40;Master Data Services&#41;](../../2014/master-data-services/change-a-business-rule-name-master-data-services.md)   
 [Configurar reglas de negocios para enviar notificaciones &#40;Master Data Services&#41;](../../2014/master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)  
  
  