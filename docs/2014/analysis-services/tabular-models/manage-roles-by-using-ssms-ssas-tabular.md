---
title: Administrar roles mediante SSMS (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 652faac0-1cfc-438b-8119-2f4b090a2381
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 098d9b589396ebd6a9c622f921efd97d0b000929
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66067036"
---
# <a name="manage-roles-by-using-ssms-ssas-tabular"></a>Administrar roles utilizando SSMS (SSAS tabular)
  Puede crear, modificar, y administrar roles para un modelo tabular implementado mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Tareas de este tema:  
  
-   [Para crear un nuevo rol](#bkmk_new_role)  
  
-   [Para copiar un rol](#bkmk_copy_role)  
  
-   [Para editar un rol](#bkmk_edit_role)  
  
-   [Para eliminar un rol](#bkmk_deletet_role)  
  
> [!CAUTION]  
>  El nuevo despliegue de un proyecto de modelos tabular con roles definidos mediante el Administrador de roles de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] sobrescribirá los roles definidos en un modelo tabular implementado.  
  
> [!CAUTION]  
>  Si se utiliza [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para administrar una base de datos del área de trabajo del modelo tabular mientras está abierto el proyecto de modelos en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] , se puede dañar el archivo Model.bim. Al crear y administrar roles para una base de datos del área de trabajo del modelo tabular, utilice el Administrador de roles de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
###  <a name="bkmk_new_role"></a>Para crear un nuevo rol  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda la base de datos de modelos tabulares en la que desee crear un rol, haga clic con el botón secundario en **Roles**y después en **Nuevo rol**.  
  
2.  En el cuadro de diálogo **Crear rol** , en la ventana Seleccionar una página, haga clic en **General**.  
  
3.  En la ventana de las opciones generales, escriba un nombre para el rol en el campo **Nombre** .  
  
     De forma predeterminada, el nombre del rol predeterminado se incrementará numéricamente para cada nuevo rol. Se recomienda escribir un nombre que identifique claramente el tipo de miembro, por ejemplo, Administradores financieros o Especialistas en recursos humanos.  
  
4.  En **Establezca los permisos de base de datos para este rol**, seleccione una de las siguientes opciones de permiso:  
  
    |Permiso|Descripción|  
    |----------------|-----------------|  
    |**Control total (Administrador)**|Los miembros pueden realizar modificaciones en el esquema del modelo y pueden ver todos los datos.|  
    |**Procesar base de datos**|Los modelos pueden ejecutar las operaciones Procesar y Procesar todo. No pueden modificar el esquema del modelo y no pueden ver los datos.|  
    |**Lectura**|Los miembros pueden ver los datos (según los filtros de fila), pero no pueden realizar cambios en el esquema del modelo.|  
  
5.  En el cuadro de diálogo **Crear rol** , en la ventana Seleccionar una página, haga clic en **Pertenencia**.  
  
6.  En la ventana de configuración de la pertenencia, haga clic en **Agregar**y en el cuadro de diálogo **Seleccionar usuarios o grupos** , agregue los usuarios o grupos de Windows que desee añadir como miembros.  
  
7.  Si el rol que va a crear tiene permisos de lectura, puede agregar filtros de fila para las tablas utilizando una fórmula DAX. Para agregar filtros de fila, en el cuadro de diálogo **propiedades de rol- \<roleName>** , en **seleccionar una página**, haga clic en **filtros de fila**.  
  
8.  En la ventana filtros de fila, seleccione una tabla, haga clic en el campo **filtro Dax** y, a continuación, en el campo **filtro dax \<-TableName>** , escriba una fórmula Dax.  
  
    > [!NOTE]  
    >  El campo filtro DAX \<-TableName> no contiene una característica del editor de consultas de autocompletar o de la función Insert. Para usar Autocompletar al escribir una fórmula DAX, debe utilizar un editor de fórmulas DAX de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
9. Haga clic en **Aceptar** para guardar el rol.  
  
###  <a name="bkmk_copy_role"></a>Para copiar un rol  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda la base de datos de modelos tabulares que contiene el rol que desea copiar, expanda **Roles**, haga clic con el botón secundario en el rol y después haga clic en **Duplicar**.  
  
###  <a name="bkmk_edit_role"></a>Para editar un rol  
  
-   En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda la base de datos de modelos tabulares que contiene el rol que desea modificar, expanda **Roles**, haga clic con el botón secundario en el rol y después haga clic en **Propiedades**.  
  
     En el cuadro de diálogo **propiedades** \<de rol roleName>, puede cambiar los permisos, agregar o quitar miembros y agregar o modificar filtros de fila.  
  
###  <a name="bkmk_deletet_role"></a>Para eliminar un rol  
  
-   En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda la base de datos de modelos tabulares que contiene el rol que desea quitar, expanda **Roles**, haga clic con el botón secundario en el rol y después haga clic en **Eliminar**.  
  
## <a name="see-also"></a>Consulte también  
 [Roles &#40;SSAS tabular&#41;](roles-ssas-tabular.md)  
  
  
