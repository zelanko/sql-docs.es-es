---
title: "Requerir valores de atributo (Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "reglas de negocios [Master Data Services], requerir valores de atributo"
  - "atributos [Master Data Services], requerir valores"
ms.assetid: a360ef13-0c34-43b8-a87e-2f5d8732d30e
caps.latest.revision: 9
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 9
---
# Requerir valores de atributo (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], requiera valores de atributo cuando desee asegurarse de que los datos maestros están completos.  
  
> [!NOTE]  
>  Los miembros que sean valores de atributos basados en dominio y que falten no se muestran en las jerarquías derivadas que se basen en esas relaciones.  
  
## Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, consulte [administradores & #40; Master Data Services & #41;](../master-data-services/administrators-master-data-services.md).  
  
### Requerir los valores de atributo  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En la barra de menús, seleccione **Administrar** y haga clic en **Reglas de negocios**.  
  
3.  En la **reglas de negocios** página, desde el **modelo** lista desplegable, seleccione un modelo.  
  
4.  Desde el **entidad** lista desplegable, seleccione una entidad.  
  
5.  Desde el **tipos de miembro** lista desplegable, seleccione un tipo de miembro de la regla de negocios para aplicar a.  
  
6.  Haga clic en **Agregar**.  
  
7.  En el cuadro **Nombre** , escriba un nombre para la regla de negocio.  
  
8.  Opcionalmente, en el campo **Descripción** , escriba la descripción de la regla de negocio.  
  
9. En el bloque **Entonces** , haga clic en **Agregar**. Se mostrará un panel.  
  
10. Desde el **operador** lista desplegable, seleccione **requiere acción**.  
  
11. Desde el **atributo** lista desplegable, seleccione un atributo.  
  
12. Haga clic en **Guardar**. Se agregará una fila nueva a la cuadrícula **Entonces** .  
  
13. Haga clic en **Guardar**.  
  
14. Haga clic en **Publish All**(Publicar todo).  
  
15. En el cuadro de diálogo de confirmación, haga clic en **Aceptar**. El valor de la columna **Business Rule State** (Estado de la regla de negocio) es **Activo**.  
  
## Pasos siguientes  
  
-   Aplique las reglas de negocios a los datos siguiendo uno de estos procedimientos:  
  
    -   [Validar a miembros específicos con reglas de negocios & #40; Master Data Services & #41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [Validar una versión con las reglas de negocios & #40; Master Data Services & #41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## Vea también  
 [Las reglas de negocios & #40; Master Data Services & #41;](../master-data-services/business-rules-master-data-services.md)   
 [Jerarquías derivadas & #40; Master Data Services & #41;](../master-data-services/derived-hierarchies-master-data-services.md)  
  
  