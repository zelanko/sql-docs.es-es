---
title: Crear un atributo de fecha (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- creating date attributes [Master Data Services]
- attributes [Master Data Services], creating date attributes
ms.assetid: 22a8f1a3-b4f2-4cfa-8495-7daad5ce9d12
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 1284a15e16465962e2ce2c286bfb2897bb297622
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "65483351"
---
# <a name="create-a-date-attribute-master-data-services"></a>Crear un atributo de fecha (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], cree un atributo de fecha cuando desee que los usuarios escriban una fecha como un valor de atributo.  
  
> [!NOTE]  
>  El atributo se denomina DateTime, pero los valores de hora no se admiten.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   Debe tener una entidad para la que crear el atributo. Para obtener más información, vea [Create an Entity &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-entity-master-data-services.md).  
  
### <a name="to-create-a-date-attribute"></a>Crear un atributo de fecha  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En la página **Vista de modelo** , en la barra de menús, seleccione **Administrar** y haga clic en **Entidades**.  
  
3.  En la página **Mantenimiento de entidades** , en la lista **Modelo** , seleccione un modelo.  
  
4.  Seleccione la fila para la entidad para la que desea crear un atributo.  
  
5.  Haga clic en **Editar entidad seleccionada**.  
  
6.  En la página **Editar entidad** :  
  
    -   Si el atributo es para miembros hoja, en el panel **Atributos de miembro hoja** , haga clic en **Agregar atributo hoja**.  
  
    -   Si el atributo es para miembros consolidados, en el panel **Atributos de miembro consolidados** , haga clic en **Agregar atributo consolidado**.  
  
    -   Si el atributo es para colecciones, en el panel **Atributos de colección** , haga clic en **Agregar atributo de colección**.  
  
7.  En la página **Agregar atributo** , seleccione la opción **Forma libre** .  
  
8.  En el cuadro **Nombre** , escriba un nombre para el atributo. Para ver una lista de palabras que no se deben usar como nombres de atributo, consulte [Palabras reservadas &#40;Master Data Services&#41;](../../2014/master-data-services/reserved-words-master-data-services.md).  
  
9. En el cuadro **Ancho de píxel de la pantalla** , escriba el ancho de la columna de atributo que se va a mostrar en la cuadrícula del **Explorador** .  
  
10. En la lista **Tipo de datos** , seleccione **DateTime**.  
  
11. En la lista **Máscara de entrada** , seleccione un formato para las fechas.  
  
12. Si lo desea, seleccione **Habilitar seguimiento de cambios** para realizar el seguimiento de los cambios en los grupos de atributos. Para obtener más información, consulte [Agregar atributos a un grupo de seguimiento de cambios &#40;Master Data Services&#41;](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md).  
  
13. Haga clic en **Guardar atributo**.  
  
14. En la página **Mantenimiento de entidades** , haga clic en **Guardar entidad**.  
  
## <a name="to-display-the-time-portion-of-a-datetime-value"></a>Para mostrar la parte de hora de un valor datetime  
 Para hacer que la interfaz de usuario muestre la parte de hora de un valor datetime, debe seleccionar una máscara de entrada apropiada para el atributo. Ninguna de las máscaras integradas para los atributos Datetime hacen esto, pero puede agregar una nueva máscara que permitirá mostrar la hora. Para ello, agregue una fila a la tabla mdm.tblList de la base de datos MDS, donde se almacenan las máscaras integradas. La fila debe tener los valores siguientes:  
  
|||  
|-|-|  
|ListCode|lstInputMask|  
|ListName|Máscara de entrada|  
|Seq|19|  
|Opción de lista|dd/MM/yyyy hh:mm:ss tt|  
|Option ID|19|  
|IsVisible|1|  
|Group_ID|3|  
  
 Después de escribir una fila con los valores anteriores en la tabla mdm.tblList, la máscara "dd/MMM/yyyy hh:mm:ss tt" estará disponible en el cuadro de lista Máscara de entrada. Entonces puede seleccionar esa máscara para mostrar la fecha y la hora de una columna de atributos datetime de una entidad en el Explorador MDS.  
  
 La Máscara de entrada es una cadena con formato de fecha y hora de .NET personalizado. Para más información, consulte [Cadenas con formato de fecha y hora personalizado](https://msdn.microsoft.com/library/8kb3ddd4\(v=vs.110\).aspx)  
  
## <a name="see-also"></a>Consulte también  
 [Atributos &#40;Master Data Services&#41;](../../2014/master-data-services/attributes-master-data-services.md)   
 [Cambiar el nombre de un atributo &#40;Master Data Services&#41;](change-an-attribute-name-and-data-type-master-data-services.md)   
 [Cree un atributo basado en dominio &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)   
 [Cree un atributo de archivo &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-file-attribute-master-data-services.md)  
  
  
