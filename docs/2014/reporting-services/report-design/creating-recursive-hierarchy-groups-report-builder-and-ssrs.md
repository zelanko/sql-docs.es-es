---
title: Creación de grupos de jerarquía recursiva (generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 06eccab6-4089-46e8-a84f-5bf3bbe0c23b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 92412bbde8a1032b34264ca254560f31704281e8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63135578"
---
# <a name="creating-recursive-hierarchy-groups-report-builder-and-ssrs"></a>Creación de grupos de jerarquía recursiva (generador de informes y SSRS)
  Para mostrar datos recursivos donde la relación entre elemento primario y secundario se representa mediante campos del conjunto de datos, puede establecer la expresión de grupo de región de datos basada en el campo secundario y establezca la propiedad Parent según el campo primario.  
  
 Mostrar datos jerárquicos es un uso común para los grupos de jerarquía recursiva, por ejemplo, los empleados en un organigrama. El conjunto de datos incluye una lista de empleados y jefes, donde los nombres de los jefes también aparecen en la lista de empleados.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="creating-recursive-hierarchies"></a>Crear jerarquías recursivas  
 Para crear una jerarquía recursiva en una región de datos tablix, debe establecer la expresión de grupo en el campo que especifica los datos secundarios y la propiedad Parent del grupo en el campo que especifica los datos primarios. Por ejemplo, para un conjunto de datos que incluya campos de employee ID y el Id. del administrador donde empleados notifican a los administradores, establezca la expresión de grupo para el Id. de empleado y la propiedad Parent en el Administrador de identificador.  
  
 Un grupo que se define como una jerarquía recursiva (es decir, un grupo que utiliza la propiedad Parent) puede tener una única expresión de grupo. Puede utilizar la función `Level` en el margen del cuadro de texto para aplicar sangría a los nombres de los empleados en función de su nivel en la jerarquía.  
  
 Para obtener más información, consulte [agregar o eliminar un grupo en una región de datos &#40;generador de informes y SSRS&#41; ](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md) y [crear un grupo de jerarquía recursiva &#40;generador de informes y SSRS&#41;](create-a-recursive-hierarchy-group-report-builder-and-ssrs.md).  
  
### <a name="aggregate-functions-that-support-recursion"></a>Funciones de agregado que admiten la recursión  
 Puede usar las funciones de agregado de Reporting Services que aceptan el parámetro *recursiva* para calcular los datos de resumen para una jerarquía recursiva. Las funciones siguientes aceptan `Recursive` como un parámetro: [Suma](report-builder-functions-sum-function.md), [Avg](report-builder-functions-avg-function.md), [recuento](report-builder-functions-count-function.md), [CountDistinct](report-builder-functions-countdistinct-function.md), [CountRows](report-builder-functions-countrows-function.md), [Max](report-builder-functions-max-function.md), [Min](report-builder-functions-min-function.md), [StDev](report-builder-functions-stdev-function.md), [StDevP](report-builder-functions-stdevp-function.md), [suma](report-builder-functions-sum-function.md), [Var](report-builder-functions-var-function.md), y [VarP](report-builder-functions-varp-function.md) . Para obtener más información, consulte [referencia a las funciones de agregado &#40;generador de informes y SSRS&#41;](report-builder-functions-aggregate-functions-reference.md).  
  
## <a name="see-also"></a>Vea también  
 [Las tablas, Matrices y listas &#40;generador de informes y SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Región de datos Tablix &#40;generador de informes y SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [Referencia a las funciones de agregado &#40;generador de informes y SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)   
 [Las tablas &#40;generador de informes y SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [Matrices &#40;generador de informes y SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [Enumera &#40;generador de informes y SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Las tablas, Matrices y listas &#40;generador de informes y SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
