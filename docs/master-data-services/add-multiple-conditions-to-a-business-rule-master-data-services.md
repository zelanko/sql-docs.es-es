---
title: Agregar varias condiciones a una regla de negocios (Master Data Services) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- business rules [Master Data Services], multiple conditions
ms.assetid: 5f0f6958-6cf2-444b-bdcd-05b887637a0b
caps.latest.revision: 9
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: be8c4995258fe2e5150a6575682988728bdae94f
ms.contentlocale: es-es
ms.lasthandoff: 09/07/2017

---
# <a name="add-multiple-conditions-to-a-business-rule-master-data-services"></a>Agregar varias condiciones a una regla de negocios (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], agregue varias condiciones **AND** u **OR** a una regla de negocio cuando quiera una regla más compleja.  
  
> [!NOTE]  
>  Si crea una regla de negocio que usa el operador **OR** , considere crear una regla distinta para cada instrucción condicional que se pueda evaluar de forma independiente. A continuación, puede excluir las reglas según sea necesario, proporcionando más flexibilidad y facilitando la solución de problemas.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Una regla de negocios debe existir. Para obtener más información, consulte [Crear y publicar una regla de negocios &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md).  
  
### <a name="to-add-multiple-conditions-to-a-business-rule"></a>Para agregar varias condiciones a una regla de negocios  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En la barra de menús, seleccione **Administrar** y haga clic en **Reglas de negocios**.  
  
3.  En la página **Reglas de negocios/** , en la lista desplegable **Modelo** , seleccione un modelo.  
  
4.  En la lista desplegable **Entidad** , seleccione una entidad.  
  
5.  En la lista desplegable **Member Types** (Tipos de miembros), seleccione un tipo de miembro.  
  
6.  Haga clic en la fila de la regla de negocios que desea modificar.  
  
7.  Haga clic en **Editar**.  
  
8.  En el bloque **If** , en el lado izquierdo de la lista desplegable de operadores lógicos, seleccione **AND/OR/ NOT**.  
  
9. Haga clic en **Agregar**. Se mostrará un panel.  
  
10. En la lista desplegable **Atributo** , seleccione un atributo.  
  
11. En la lista desplegable **Operador** , seleccione una condición.  
  
12. Complete todos los campos obligatorios.  
  
13. Haga clic en **Guardar**. Se agregará una fila nueva a la cuadrícula **Si** .  
  
14. Opcionalmente, para agregar más condiciones, complete los pasos 8 al 13.  
  
    > [!TIP]  
    >  Para eliminar una condición, selecciónela, haga clic con el botón derecho en ella y, después, haga clic en **Eliminar**.  
  
    > [!TIP]  
    >  Puede seleccionar varias condiciones y haga clic con el botón derecho para agruparlas en un operador lógico o para desagrupar las condiciones dentro de un operador lógico específico.  
  
## <a name="see-also"></a>Vea también  
 [Reglas de negocios &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)   
 [Cambiar el nombre de una regla de negocios &#40;Master Data Services&#41;](../master-data-services/change-a-business-rule-name-master-data-services.md)   
 [Configurar reglas de negocios para enviar notificaciones &#40;Master Data Services&#41;](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)  
  
  

