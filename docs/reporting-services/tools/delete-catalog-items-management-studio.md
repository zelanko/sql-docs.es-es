---
title: Eliminar elementos del catálogo (Management Studio) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.deleteitems.f1
ms.assetid: b0599e01-6dc3-4484-80d4-022a412e0ebd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b8576a1946368c7adc1a32aa66ce44e28603616a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65573935"
---
# <a name="delete-catalog-items-management-studio"></a>Eliminar elementos del catálogo (Management Studio)
  Utilice esta página para eliminar programaciones compartidas y definiciones de roles.  
  
 Si elimina una programación compartida usada por varios informes y suscripciones, el servidor de informes creará calendarios individuales para cada informe y suscripción que haya usado anteriormente la programación compartida. Cada nueva programación individual contendrá la fecha, la hora y el patrón de periodicidad que se especificó en la programación compartida. Tenga en cuenta que [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no proporciona la administración central de las programaciones individuales. Si elimina una programación compartida, tendrá que mantener ahora la información de programación para cada elemento individual. Antes de eliminar una programación compartida, use la [página Informes](../../reporting-services/tools/schedule-properties-reports-page.md) para determinar qué informes usan actualmente la programación compartida.  
  
 Para las definiciones de roles, solo se pueden eliminar las que no se usan en una asignación de roles activamente. Si intenta eliminar un rol que se encuentra actualmente en uso, el servidor de informes no eliminará el rol y verá un mensaje de error para dicho efecto. Si esta página contiene una definición de roles única que no se encuentra actualmente en uso, se eliminará al hacer clic en **Aceptar**. Si esta página contiene varios roles, no puede seleccionar qué roles desea mantener o quitar. Se eliminarán todas las definiciones de roles no usadas al hacer clic en **Aceptar**.  
  
 No puede deshacer una operación de eliminación. Si desea recuperar un elemento eliminado, debe volver a crearlo o restaurar una copia de seguridad de la base de datos de servidor de informes.  
  
## <a name="options"></a>Opciones  
 **Nombre**  
 Especifica el nombre del elemento que va a eliminar.  
  
 **Tipo**  
 Muestra el tipo de elemento que va a eliminar.  
  
 **Propietario**  
 Muestra el nombre del propietario. En la mayoría de los casos, es Sistema.  
  
 **Estado**  
 Muestra información de progreso de una operación de eliminación.  
  
 **Error**  
 Muestra un código de error si se produce un error al eliminar un elemento.  
  
## <a name="see-also"></a>Consulte también  
 [Eliminar un elemento &#40;Management Studio&#41;](../../reporting-services/tools/delete-an-item-management-studio.md)   
 [Servidor de informes en Management Studio ayuda F1](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Crear, modificar y eliminar programaciones](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md)  
  
  
