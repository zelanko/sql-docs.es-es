---
title: Crear y administrar Roles (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.rolemanager.f1
- sql12.asvs.bidtoolset.roledb.f1
ms.assetid: e23d27a8-e968-4082-9dbe-963fc724b5d9
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 10e5e26142cd1819e4f2c5f884af9c2f2af10812
ms.sourcegitcommit: 0818f6cc435519699866db07c49133488af323f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284906"
---
# <a name="create-and-manage-roles-ssas-tabular"></a>Crear y administrar roles (SSAS tabular)
  Los roles, en los modelos tabulares, definen los permisos de los miembros para un modelo. Los roles se definen para un proyecto de modelos mediante el cuadro de diálogo Administrador de roles de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Al implementar un modelo, los administradores de bases de datos pueden administrar los roles mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Las tareas de este tema explican cómo crear y administrar roles durante la creación de modelos mediante el cuadro de diálogo Administrador de roles en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para obtener información sobre cómo administrar roles en una base de datos modelo implementada, vea [Roles de modelos tabulares &#40;SSAS tabular&#41;](roles-ssas-tabular.md).  
  
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
    >  También se pueden agregar miembros de rol a un modelo implementado mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para más información, vea [Administrar roles usando SSMS &#40;SSAS tabular&#41;](manage-roles-by-using-ssms-ssas-tabular.md).  
  
8.  En el cuadro de diálogo **Seleccionar usuarios o grupos** , especifique el usuario de Windows o los objetos de grupo de Windows como miembros.  
  
9. Haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Roles &#40;SSAS tabular&#41;](roles-ssas-tabular.md)   
 [Perspectivas &#40;SSAS tabular&#41;](perspectives-ssas-tabular.md)   
 [Analizar en Excel &#40;SSAS tabular&#41;](analyze-in-excel-ssas-tabular.md)   
 [Función USERNAME &#40;DAX&#41;](/dax/username-function-dax)   
 [Función CUSTOMDATA &#40;DAX&#41;](/dax/customdata-function-dax)  
  
  
