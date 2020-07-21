---
title: Iniciar acciones según los cambios de valores de atributos (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], tracking attribute changes
- change tracking groups [Master Data Services], initiating actions
ms.assetid: 5e4402ce-31db-4774-a2a1-552335f87693
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 4dffc314c99345c9e8db632fbcebc1f2e3653d2f
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971365"
---
# <a name="initiate-actions-based-on-attribute-value-changes-master-data-services"></a>Iniciar acciones según los cambios de valores de atributos (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], cree una regla de negocios para iniciar acciones según los cambios de los valores de atributos. Por ejemplo, cuando un valor de atributo concreto cambia, quizás desee cambiar un valor, enviar una notificación o iniciar un flujo de trabajo externo.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   Los atributos deben estar en un grupo de seguimiento de cambios. Consulte [Agregar atributos a un grupo de seguimiento de cambios &#40;Master Data Services&#41;](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md) para obtener más información.  
  
### <a name="to-create-a-business-rule-to-initiate-actions-based-on-attribute-value-changes"></a>Crear una regla de negocios para iniciar acciones según los cambios de los valores de atributos  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En la barra de menús, seleccione **Administrar** y haga clic en **Reglas de negocios**.  
  
3.  En la página **Mantenimiento de reglas de negocios** , en la lista **Modelo** , seleccione un modelo.  
  
4.  En la lista **Entidad** , seleccione una entidad.  
  
5.  En la lista **Tipo de miembro** , seleccione un tipo de miembro al que aplicar la regla de negocios.  
  
6.  En la lista **Atributo** , seleccione un atributo o deje el valor predeterminado de **Todos**.  
  
7.  Haga clic en **Agregar regla de negocios**.  
  
8.  Haga clic en **Editar regla de negocios seleccionada**.  
  
9. En el panel **Componentes** , expanda el nodo **Condiciones** .  
  
10. En el nodo **Comparación de valor** , arrastre **ha cambiado** hasta la etiqueta **Condiciones** del panel **IF** .  
  
11. En el panel **atributos** , haga clic en un atributo y arrástrelo hasta la etiqueta **seleccionar atributo** del panel **Editar condición** . Este atributo no tiene ningún efecto en la regla, así que seleccione cualquiera disponible.  
  
12. En el panel **Editar condición** , en el cuadro **Grupo de seguimientos de cambios** , escriba el número del grupo de seguimiento de cambios que asignó como parte de los requisitos previos.  
  
13. En el panel **Editar acción** , haga clic en **Guardar elemento**.  
  
14. En el panel **Componentes** , expanda el nodo **Acciones** .  
  
15. Haga clic en una acción y arrástrela hasta la etiqueta **Acción** del panel **THEN** .  
  
16. En el panel **Atributos** , haga clic en un atributo y arrástrelo hasta la etiqueta **Seleccionar atributo** del panel **Editar acción** .  
  
17. En el panel **Editar acción** , complete los campos obligatorios.  
  
18. En el panel **Editar acción** , haga clic en **Guardar elemento**.  
  
19. Haga clic en **Atrás**.  
  
20. Opcionalmente, en la página **Business Rules Maintenance** (Mantenimiento de las reglas de negocios), en la fila que contiene la regla de negocio, haga doble clic en una celda de las columnas **Nombre**, **Descripción**o **Notificación** para actualizar el valor.  
  
    > [!NOTE]  
    >  Las notificaciones solo se envían para las reglas que incluyen una acción de validación.  
  
21. Haga clic en **Publicar reglas de negocios**.  
  
22. En el cuadro de diálogo de confirmación, haga clic en **Aceptar**. El estado de la regla cambia a **Activo**.  
  
## <a name="next-steps"></a>Pasos siguientes  
  
-   Aplique las reglas de negocios a los datos siguiendo uno de estos procedimientos:  
  
    -   [Validar miembros específicos con las reglas de negocios &#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [Validar una versión con las reglas de negocios &#40;Master Data Services&#41;](../../2014/master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>Consulte también  
 [Agregar atributos a un grupo de Change Tracking &#40;Master Data Services&#41;](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)   
 [Reglas de negocios &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
  
