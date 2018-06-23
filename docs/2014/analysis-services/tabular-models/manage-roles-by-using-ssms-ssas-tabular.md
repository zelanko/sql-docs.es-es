---
title: Administrar Roles utilizando SSMS (SSAS Tabular) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 652faac0-1cfc-438b-8119-2f4b090a2381
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 907b1ea2b655c9da1b9754441be5a933ac8380af
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113007"
---
# <a name="manage-roles-by-using-ssms-ssas-tabular"></a>Administrar roles utilizando SSMS (SSAS tabular)
  Puede crear, modificar, y administrar roles para un modelo tabular implementado mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Tareas en este tema:  
  
-   [Para crear un rol](#bkmk_new_role)  
  
-   [Para copiar un rol](#bkmk_copy_role)  
  
-   [Para modificar un rol](#bkmk_edit_role)  
  
-   [Para eliminar un rol](#bkmk_deletet_role)  
  
> [!CAUTION]  
>  El nuevo despliegue de un proyecto de modelos tabular con roles definidos mediante el Administrador de roles de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] sobrescribirá los roles definidos en un modelo tabular implementado.  
  
> [!CAUTION]  
>  Si se utiliza [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para administrar una base de datos del área de trabajo del modelo tabular mientras está abierto el proyecto de modelos en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] , se puede dañar el archivo Model.bim. Al crear y administrar roles para una base de datos del área de trabajo del modelo tabular, utilice el Administrador de roles de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
###  <a name="bkmk_new_role"></a> Para crear un rol  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda la base de datos de modelos tabulares en la que desee crear un rol, haga clic con el botón secundario en **Roles**y después en **Nuevo rol**.  
  
2.  En el cuadro de diálogo **Crear rol** , en la ventana Seleccionar una página, haga clic en **General**.  
  
3.  En la ventana de las opciones generales, escriba un nombre para el rol en el campo **Nombre** .  
  
     De forma predeterminada, el nombre del rol predeterminado se incrementará numéricamente para cada nuevo rol. Se recomienda escribir un nombre que identifique claramente el tipo de miembro, por ejemplo, Administradores financieros o Especialistas en recursos humanos.  
  
4.  En **Establezca los permisos de base de datos para este rol**, seleccione una de las siguientes opciones de permiso:  
  
    |Permiso|Descripción|  
    |----------------|-----------------|  
    |**Control total (Administrador)**|Los miembros pueden realizar modificaciones en el esquema del modelo y pueden ver todos los datos.|  
    |**Procesar base de datos**|Los miembros pueden ejecutar las operaciones Procesar y Procesar todo. No pueden modificar el esquema del modelo y no pueden ver los datos.|  
    |**Lectura**|Los miembros pueden ver los datos (según los filtros de fila), pero no pueden realizar cambios en el esquema del modelo.|  
  
5.  En el cuadro de diálogo **Crear rol** , en la ventana Seleccionar una página, haga clic en **Pertenencia**.  
  
6.  En la ventana de configuración de la pertenencia, haga clic en **Agregar**y en el cuadro de diálogo **Seleccionar usuarios o grupos** , agregue los usuarios o grupos de Windows que desee añadir como miembros.  
  
7.  Si el rol que va a crear tiene permisos de lectura, puede agregar filtros de fila para las tablas utilizando una fórmula DAX. Para agregar filtros de fila en la **propiedades de función: \<rolename >** cuadro de diálogo **seleccionar una página**, haga clic en **filtros de fila**.  
  
8.  En la ventana de filtros de fila, seleccione una tabla y, a continuación, haga clic en el **filtro DAX** campo y, a continuación, en la **filtro DAX - \<tablename >** , escriba una fórmula DAX.  
  
    > [!NOTE]  
    >  El filtro DAX - \<tablename > campo no contiene un editor de consultas de Autocompletar o característica de Insertar función. Para usar Autocompletar al escribir una fórmula DAX, debe utilizar un editor de fórmulas DAX de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
9. Haga clic en **Aceptar** para guardar el rol.  
  
###  <a name="bkmk_copy_role"></a> Para copiar un rol  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda la base de datos de modelos tabulares que contiene el rol que desea copiar, expanda **Roles**, haga clic con el botón secundario en el rol y después haga clic en **Duplicar**.  
  
###  <a name="bkmk_edit_role"></a> Para modificar un rol  
  
-   En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda la base de datos de modelos tabulares que contiene el rol que desea modificar, expanda **Roles**, haga clic con el botón secundario en el rol y después haga clic en **Propiedades**.  
  
     En el **propiedades de la función** \<rolename > cuadro de diálogo, puede cambiar los permisos, agregar o quitar miembros, y agregar o modificar filtros de fila.  
  
###  <a name="bkmk_deletet_role"></a> Para eliminar un rol  
  
-   En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda la base de datos de modelos tabulares que contiene el rol que desea quitar, expanda **Roles**, haga clic con el botón secundario en el rol y después haga clic en **Eliminar**.  
  
## <a name="see-also"></a>Vea también  
 [Roles &#40;SSAS Tabular&#41;](roles-ssas-tabular.md)  
  
  