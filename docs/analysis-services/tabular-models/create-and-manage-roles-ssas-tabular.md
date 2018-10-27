---
title: Crear y administrar Roles | Microsoft Docs
ms.date: 09/17/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 883eab47796f5cb09d5993fa2b2570cdda3cd2ae
ms.sourcegitcommit: 9f2edcdf958e6afce9a09fb2e572ae36dfe9edb0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2018
ms.locfileid: "50099656"
---
# <a name="create-and-manage-roles"></a>Crear y administrar roles 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Los roles, en los modelos tabulares, definen los permisos de los miembros para un modelo. Los roles se definen para un proyecto de modelos mediante el cuadro de diálogo Administrador de roles de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. 

> [!IMPORTANT]
> Si va a implementar el proyecto en Azure Analysis Services, use **área de trabajo integrada** como la base de datos del área de trabajo. Para obtener más información, consulte [base de datos del área de trabajo](workspace-database-ssas-tabular.md).
  
 Las tareas de este artículo describen cómo crear y administrar roles durante la creación del modelo mediante el cuadro de diálogo Administrador de roles [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para obtener información sobre cómo administrar roles en una base de datos de modelo implementada, vea [Roles de modelos tabulares](../../analysis-services/tabular-models/tabular-model-roles-ssas-tabular.md).  
  
## <a name="tasks"></a>Tareas  
 Para crear, modificar, copiar y eliminar roles, utilice el cuadro de diálogo **Administrador de roles** . Para ver el cuadro de diálogo **Administrador de roles** , en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], haga clic en el menú **Modelo** y en **Administrador de roles**.  
  
###  <a name="bkmk_new_role"></a> Para crear un rol  
  
1.  En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], haga clic en el menú **Modelo** y en **Administrador de roles**.  
  
2.  En el cuadro de diálogo **Administrador de roles** , haga clic en **Nuevo**.  
  
     Se agregará un nuevo rol resaltado a la lista de roles.  
  
3.  En la lista **Roles** , en el campo **Nombre** , escriba un nombre para el rol.  
  
     De forma predeterminada, el nombre del rol predeterminado se incrementará numéricamente para cada nuevo rol. Se recomienda escribir un nombre que identifique claramente el tipo de miembro, por ejemplo, Administradores financieros o Especialistas en recursos humanos.  
  
4.  En el campo **Permisos** , haga clic en la flecha abajo y seleccione uno de los tipos de permisos siguientes:  
  
    |Permiso|Descripción|  
    |----------------|-----------------|  
    |**Ninguno**|Los miembros no pueden realizar ninguna modificación en el esquema del modelo y no pueden consultar los datos.|  
    |**Lectura**|Los miembros pueden consultar los datos (según los filtros de fila), pero no pueden realizar cambios en el esquema del modelo.|  
    |**Leer y actualizar**|Los miembros pueden actualizar los datos (según los filtros de fila) y ejecutar las operaciones Procesar y Procesar todo, pero no pueden realizar cambios en el esquema del modelo.|  
    |**Procesar**|Los miembros pueden ejecutar las operaciones Procesar y Procesar todo. No pueden modificar el esquema del modelo y no pueden consultar los datos.|  
    |**Administrador**|Los miembros pueden realizar modificaciones en el esquema del modelo y pueden consultar todos los datos.|  
  
5.  Para especificar una descripción para el rol, haga clic en el campo **Descripción** y escriba una descripción.  
  
6.  Si el rol que está creando tiene permiso de lectura o de lectura y procesamiento, puede agregar filtros de fila mediante una fórmula de DAX. Para agregar filtros de fila, haga clic en la pestaña **Filtros de fila** , seleccione una tabla, haga clic en el campo **Filtro DAX** y, a continuación, escriba una fórmula de DAX.  
  
7.  Para agregar miembros al rol, haga clic en la pestaña **Miembros** y, a continuación, haga clic en **Agregar**.  
  
    > [!NOTE]  
    >  También se pueden agregar miembros de rol a un modelo implementado mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obtener más información, consulte [administrar Roles utilizando SSMS](../../analysis-services/tabular-models/manage-roles-by-using-ssms-ssas-tabular.md).  
  
8.  En el cuadro de diálogo **Seleccionar usuarios o grupos** , especifique el usuario de Windows o los objetos de grupo de Windows como miembros.  
  
9. Haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)   
 [Perspectivas](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Analizar en Excel](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)   
 [Función USERNAME (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f)   
 [Función CUSTOMDATA (DAX)](http://msdn.microsoft.com/58235ad8-226c-43cc-8a69-5a52ac19dd4e)  
  
  
