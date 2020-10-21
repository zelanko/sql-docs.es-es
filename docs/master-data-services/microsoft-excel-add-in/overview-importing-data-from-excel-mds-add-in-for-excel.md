---
description: 'Introducción: Importación de datos de Excel (complemento MDS para Excel)'
title: Importar datos de Excel
ms.custom: microsoft-excel-add-in
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: ea84a9aa-aeec-411b-ab8d-bc1b14f864a3
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: df78497bc65d383a3dc44225971ab1df742f32b5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "92257798"
---
# <a name="overview-importing-data-from-excel-mds-add-in-for-excel"></a>Introducción: Importación de datos de Excel (complemento MDS para Excel)

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  En [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], puede publicar los datos en el repositorio MDS si desea compartirlo con otros usuarios. En cuanto se publiquen los datos, estarán disponibles para otros usuarios del complemento para su descarga.  
  
 Al publicar datos, todos los que haya agregado o actualizado se publican en el repositorio MDS. Los datos que haya eliminado no se publican y se deben eliminar por separado. Para obtener más información, consulte [Eliminar una fila &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/delete-a-row-mds-add-in-for-excel.md).  
  
> [!NOTE]  
>  La publicación no se puede usar para crear una entidad nueva. Para obtener más información sobre cómo crear entidades, consulte [Crear una entidad &#40;Complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/create-an-entity-mds-add-in-for-excel.md).  
  
## <a name="when-multiple-users-publish-at-the-same-time"></a>Cuando varios usuarios publican simultáneamente  
 Varios usuarios pueden publicar actualizaciones de los mismos datos. A medida que cada usuario publica, la actualización se guarda en la base de datos. Esto significa que un usuario que no estaba trabajando con los datos actualizados más recientemente podrá cambiar el valor cuando los publique.  
  
 Solo las actualizaciones que se realizan se publican en la base de datos. Los datos obsoletos de la hoja de cálculo no se publican.  
  
## <a name="transactions-and-annotations"></a>Transacciones y anotaciones  
 Cada cambio publicado se guarda como una transacción. Si lo desea, puede agregar anotaciones (comentarios) a una transacción para explicar por qué se realizó el cambio.  
  
-   No puede anotar las eliminaciones, aunque se guardan como transacciones que un administrador puede invertir.  
  
-   Si cambia el valor de **Code** de un miembro, todas las transacciones anteriores del miembro pasarán a ser no disponibles. Si se devuelve el valor de **Code** al valor original, podrá obtener acceso a las transacciones anteriores.  
  
-   Puede ver las transacciones realizadas por otros usuarios en un miembro. También puede ver todas las transacciones que ha realizado en un miembro, aunque ya no tenga permiso para atributos concretos. No se pueden ver las transacciones que implican atributos en los que su permiso esté establecido en denegar.  
  
 Puede ver todas las transacciones realizadas en un miembro. Para obtener más información, consulte [Ver todas las anotaciones o transacciones de un miembro &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md).  
  
> [!IMPORTANT]  
>  Si especifica una anotación de más de 500 caracteres, se trunca automáticamente.  
  
## <a name="business-rule-and-other-validation"></a>Regla de negocios y otras validaciones  
 Al publicar datos, se realiza la validación para asegurarse de que los datos son precisos antes de agregarlos al repositorio MDS. Si los datos no cumplen los criterios especificados, no se publicarán en el repositorio. Para obtener más información, consulte [Validar datos &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/validating-data-mds-add-in-for-excel.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Publicar de nuevo los datos de la hoja de cálculo activa en el repositorio MDS.|[Importación de datos de Excel en Master Data Services &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)|  
|Eliminar una fila del repositorio MDS y de la hoja de cálculo al mismo tiempo.|[Eliminar una fila &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/delete-a-row-mds-add-in-for-excel.md)|  
|Vea las anotaciones (comentarios) y las transacciones de las filas de datos (miembros) cuando desee ver actualizaciones de los datos a través del tiempo.|[Ver todas las anotaciones o transacciones de un miembro &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)|  
|Combine los datos de dos hojas de cálculo si desea comparar los datos antes de publicarlos.|[Combinar datos &#40;Complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/combine-data-mds-add-in-for-excel.md)|  

  
## <a name="related-content"></a>Contenido relacionado  
  
-   [Actualizar datos &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/refreshing-data-mds-add-in-for-excel.md)  
  
-   [Complemento Master Data Services para Microsoft Excel](../../master-data-services/microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md)  
  
  
