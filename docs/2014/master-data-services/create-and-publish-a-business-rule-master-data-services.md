---
title: Crear y publicar una regla de negocios (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], creating
- creating business rules [Master Data Services]
ms.assetid: 6961d636-4d69-468e-81f7-8d0be6a4a039
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: dade621e2dc095ee08a803351f6692d4c4a5cc34
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227025"
---
# <a name="create-and-publish-a-business-rule-master-data-services"></a>Crear y publicar una regla de negocios (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], cree una regla de negocios para asegurarse de la exactitud de los datos maestros. Después de crear una regla, debe publicarla antes de poder aplicarla a los datos.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-create-and-publish-a-business-rule"></a>Crear y publicar una regla de negocios  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En la barra de menús, seleccione **Administrar** y haga clic en **Reglas de negocios**.  
  
3.  En la página **Mantenimiento de reglas de negocios** , en la lista **Modelo** , seleccione un modelo.  
  
4.  En la lista **Entidad** , seleccione una entidad.  
  
5.  En la lista **Tipo de miembro** , seleccione un tipo de miembro al que aplicar la regla de negocios.  
  
6.  En la lista **Atributo** , seleccione un atributo o deje el valor predeterminado de **Todos**.  
  
7.  Haga clic en **Agregar regla de negocios**.  
  
8.  Haga clic en **Editar regla de negocios seleccionada**.  
  
9. En el panel **Componentes** , expanda el nodo **Condiciones** .  
  
10. Haga clic en una condición y arrástrela hasta la **IF** del panel **condiciones** etiqueta.  
  
    > [!TIP]  
    >  Puede eliminar elementos de la regla de negocio con el botón secundario y eligiendo **eliminar**.  
  
11. En el **atributos** panel, haga clic en un atributo y arrástrelo hasta el **Editar condición** del panel **Seleccionar atributo** etiqueta.  
  
12. En el **Editar condición** panel, complete los campos obligatorios.  
  
13. En el panel **Editar acción** , haga clic en **Guardar elemento**.  
  
14. En el panel **Componentes** , expanda el nodo **Acciones** .  
  
15. Haga clic en una acción y arrástrela hasta la etiqueta **Acción** del panel **THEN** .  
  
16. En el panel **Atributos** , haga clic en un atributo y arrástrelo hasta la etiqueta **Seleccionar atributo** del panel **Editar acción** .  
  
17. En el panel **Editar acción** , complete los campos obligatorios.  
  
18. En el panel **Editar acción** , haga clic en **Guardar elemento**.  
  
19. Opcionalmente, agregue varias condiciones a la regla. Para obtener más información, vea [Agregar varias condiciones a una regla de negocios &#40;Master Data Services&#41;](../../2014/master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md).  
  
20. Haga clic en **Atrás**.  
  
21. Opcionalmente, en la página **Business Rules Maintenance** (Mantenimiento de las reglas de negocios), en la fila que contiene la regla de negocio, haga doble clic en una celda de las columnas **Nombre**, **Descripción**o **Notificación** para actualizar el valor.  
  
    > [!NOTE]  
    >  Las notificaciones solo se envían para las reglas que incluyen una acción de validación.  
  
22. Haga clic en **Publicar reglas de negocios**.  
  
23. En el cuadro de diálogo de confirmación, haga clic en **Aceptar**. El estado de la regla cambia a **Activo**.  
  
## <a name="next-steps"></a>Pasos siguientes  
  
-   Aplique las reglas de negocios a los datos siguiendo uno de estos procedimientos:  
  
    -   [Validar miembros específicos con las reglas de negocios &#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [Validar una versión con las reglas de negocios &#40;Master Data Services&#41;](../../2014/master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>Vea también  
 [Configurar reglas de negocios para enviar notificaciones &#40;Master Data Services&#41;](../../2014/master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)   
 [Cambiar el nombre de una regla de negocios &#40;Master Data Services&#41;](../../2014/master-data-services/change-a-business-rule-name-master-data-services.md)   
 [Agregar varias condiciones a una regla de negocios &#40;Master Data Services&#41;](../../2014/master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md)  
  
  
