---
title: Cambar el tipo de atributo (complemento MDS para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9d3001d9-8d0f-4e4a-8e04-4f666bf0df69
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 4406eb225002bbf5df93f8c67385694922d7d2c7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "65482762"
---
# <a name="change-the-attribute-type-mds-add-in-for-excel"></a>Cambar el tipo de atributo (complemento MDS para Excel)
  En el [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], los administradores pueden cambiar el tipo de atributo cuando el tipo de datos o el número de caracteres permitido sea incorrecto.  
  
 Si quiere cambiar el tipo de atributo para crear una lista restringida (atributo basado en dominios), consulte [Crear un atributo basado en dominio &#40;complemento MDS para Excel&#41;](create-a-domain-based-attribute-mds-add-in-for-excel.md).  
  
> [!NOTE]  
>  No se puede actualizar el tipo o la longitud de las columnas **Nombre** o **Código**.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para realizar este procedimiento:  
  
-   Debe disponer del permiso para tener acceso a las áreas funcionales del **Explorador** y de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../administrators-master-data-services.md).  
  
-   Debe haber un modelo, una entidad y un atributo existentes.  
  
### <a name="to-change-the-attribute-type"></a>Para cambiar el tipo de atributo  
  
1.  En Excel, cargue la entidad que contenga la columna (atributo) que desee cambiar. Para obtener más información, consulte [carga de datos de MDS en Excel](export-data-to-excel-from-master-data-services.md).  
  
2.  Haga clic en cualquier celda en la columna que desee cambiar.  
  
3.  En el grupo **Compilar modelo** , haga clic en **Propiedades de atributo**.  
  
4.  En el cuadro de diálogo **Propiedades de atributo** , actualice los valores según sea necesario.  
  
5.  Haga clic en **OK**.  
  
## <a name="what-happens-when-you-change-the-attribute-type"></a>¿Qué ocurre cuando se cambia el tipo de atributo?  
 Si hay alguna dependencia en el atributo, como si una regla de negocios de MDS hace referencia al atributo o si el atributo se incluye en una vista de suscripción, y cambia el tipo de datos de un atributo, MDS hará lo siguiente:  
  
-   Cambiar el tipo de datos del atributo.  
  
-   Genere una copia del atributo con el sufijo "_old" que no contenga ningún valor. Esto se denomina atributo **desusado** .  
  
 Sin embargo, todas las dependencias existentes en el atributo original apuntarán al atributo desusado, no al modificado.  
  
 Esto implica lo siguiente:  
  
-   Debe actualizar las reglas de negocios para que apunten al atributo modificado, ya que la lógica puede no ser la misma dado el nuevo tipo de datos del atributo. Tendrá que editar todas las reglas afectadas y hacer que las expresiones que apuntan a referencias quitadas del atributo desusado (_old) apunten al atributo actualizado.  
  
-   Debe abrir cualquier vista de suscripción en la selección de administración de integración, seleccionar la fila de la vista, abrirla para su edición haciendo clic en el icono de lápiz y, a continuación, hacer clic en el icono **Guardar disco** para actualizar la definición de la vista. No es necesario hacer ningún otro cambio para regenerar la sintaxis de la vista.  
  
-   En las tablas de ensayo que incluyen el atributo se agregará una columna de atributo desusado, lo que significa que el código de ensayo se verá afectado. Para deshacerse del atributo desusado, puede eliminarlo después de haber actualizado las reglas de negocios y las vistas de suscripción.  
  
 **Eliminar el atributo desusado**  
  
 Antes de eliminar cualquier atributo desusado, debe quitar las referencias al mismo, como corregir las reglas de negocios y regenerar las vistas de suscripción como se ha descrito anteriormente. De lo contrario, cuando intente eliminar el atributo desusado obtendrá un error en la página web Administración del sistema que indica que no se puede eliminar el atributo porque un objeto hace referencia a él.  
  
 Para eliminar un atributo, consulte [eliminar un atributo &#40;Master Data Services&#41;](../delete-an-attribute-master-data-services.md)  
  
> [!TIP]  
>  Es tedioso cambiar los tipos de datos de los atributos de MDS que tienen datos y entidades relacionadas existentes, especialmente si se ha declarado una regla de negocios o una vista de suscripción que depende de la entidad. La práctica recomendada es empezar con un tipo de datos que sea suficientemente flexible como para contener los valores necesarios. Por ejemplo, las cadenas pueden ser pequeñas al principio, pero quizás haya que agrandarlas con el tiempo, por lo que debe considerar los escenarios de caso peor. La longitud adicional de las cadenas de texto puede ser molesta (por ejemplo, es difícil encajar en la pantalla cuadros de texto anchos de la GUI), por lo que debe evitar una longitud grande de las cadenas.  
  
## <a name="see-also"></a>Consulte también  
 [Atributos &#40;Master Data Services&#41;](../attributes-master-data-services.md)   
 [Generar un modelo &#40;Complemento MDS para Excel&#41;](building-a-model-mds-add-in-for-excel.md)  
  
  
