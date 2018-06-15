---
title: Analizar un modelo tabular en Excel | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b1db764052a9c3370554a6456dc005612a2e8b95
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34040672"
---
# <a name="analyze-a-tabular-model-in-excel"></a>Analizar un modelo tabular en Excel  
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  La característica Analizar en Excel de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] abre Microsoft Excel, crea una conexión de origen de datos con la base de datos del área de trabajo del modelo y agrega una tabla dinámica a la hoja de cálculo. Los objetos del modelo (tablas, columnas, medidas, jerarquías y KPI) se incluyen como campos en la lista de campos de la tabla dinámica.  
  
> [!NOTE]  
>  Para usar la característica Analizar en Excel, tiene que tener instalado Microsoft Office 2003 o posterior en el mismo equipo que [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Si Office no está instalado en el mismo equipo, puede usar Excel en otro equipo y conectarse a la base de datos del área de trabajo del modelo como un origen de datos. A continuación, podrá agregar manualmente una tabla dinámica a la hoja de cálculo. Los objetos del modelo (tablas, columnas, medidas y KPI) se incluyen como campos en la lista de campos de la tabla dinámica.  
  
## <a name="tasks"></a>Tareas  
  
#### <a name="to-analyze-a-tabular-model-project-by-using-the-analyze-in-excel-feature"></a>Para analizar un proyecto de modelo tabular mediante la característica Analizar en Excel  
  
1.  En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], haga clic en el menú **Modelo** y después en **Analizar en Excel**.  
  
2.  En el cuadro de diálogo **Elegir credenciales y perspectivas** , seleccione una de las opciones de credenciales siguientes para conectarse al origen de datos del área de trabajo del modelo:  
  
    -   Para usar la cuenta de usuario actual, seleccione **Usuario de Windows actual**.  
  
    -   Para usar una cuenta de usuario diferente, seleccione **Otro usuario de Windows**.  
  
         Normalmente, esta cuenta de usuario será un miembro de un rol. No se requiere una contraseña. La cuenta solo se puede utilizar en el contexto de una conexión de Excel a la base de datos del área de trabajo.  
  
    -   Para usar un rol de seguridad, seleccione **Rol**y, a continuación, en el cuadro de lista, seleccione uno o varios roles.  
  
         Los roles de seguridad se deben definir mediante el Administrador de roles. Para obtener más información, consulte [crear y administrar funciones](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md).  
  
3.  Para usar una perspectiva, seleccione una en el cuadro de lista **Perspectiva** .  
  
     Las perspectivas (distintas de las predeterminadas) se deben definir mediante el cuadro de diálogo Perspectivas. Para obtener más información, consulte [crear y administrar perspectivas](../../analysis-services/tabular-models/create-and-manage-perspectives-ssas-tabular.md).  
  
> [!NOTE]  
>  La lista de campos de tabla dinámica de Excel no se actualiza automáticamente a medida que se realizan cambios en el proyecto de modelos en el diseñador de modelos. Para actualizar dicha lista, en Excel, haga clic en **Actualizar** en la cinta **Opciones**.  
  
## <a name="see-also"></a>Vea también  
 [Analizar en Excel](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)  
  
  
