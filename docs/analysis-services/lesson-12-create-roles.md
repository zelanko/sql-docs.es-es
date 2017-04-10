---
title: "Lecci&#243;n 12: Crear roles | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 984face4-00fc-46d3-8ae1-9755bf737bdf
caps.latest.revision: 17
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Lecci&#243;n 12: Crear roles
En esta lección, creará roles. Los roles proporcionan seguridad a los objetos y datos de la base de datos del modelo limitando el acceso únicamente a los usuarios de Windows que sean miembros del rol. Cada rol se define con un permiso único: Ninguno, Lectura, Lectura y proceso, Proceso o Administrador. Los roles se pueden definir durante la creación del modelo mediante el cuadro de diálogo Administrador de roles de [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Una vez implementado un modelo, los roles se pueden administrar con [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Para obtener más información, consulte [Roles &#40;SSAS tabular&#41;](../analysis-services/tabular-models/roles-ssas-tabular.md).  
  
> [!NOTE]  
> No es necesario crear roles para completar este tutorial. De forma predeterminada, la cuenta con la que ha iniciado sesión tendrá privilegios Administrador para el modelo. Sin embargo, para permitir que otros usuarios de su organización examinen el modelo utilizando una aplicación cliente de informes, debe crear al menos un rol con permisos de lectura y agregar esos usuarios como miembros.  
  
Creará tres roles:  
  
-   Jefe de ventas: este rol puede incluir a los usuarios de la organización a los que desea otorgar permiso de lectura para todos los objetos y datos del modelo.  
  
-   Analista de ventas EE. UU.: este rol puede incluir a los usuarios de la organización que desea que solo puedan examinar los datos relacionados con las ventas en EE. UU. Para este rol, usará una fórmula DAX para definir un *Filtro de fila*, que restringe los miembros para que solo examinen los datos correspondientes a Estados Unidos.  
  
-   Administrador: este rol puede incluir a los usuarios a los que desea otorgar el permiso Administrador, que permite acceso y permisos ilimitados para realizar tareas administrativas en la base de datos del modelo.  
  
Dado que las cuentas de usuario y grupo de Windows de su organización son únicas, puede agregar cuentas de su propia organización a los miembros. Sin embargo, para este tutorial, también puede dejar los miembros en blanco. Todavía podrá probar el efecto de cada rol más adelante en la lección 12: Analizar en Excel.  
  
Tiempo estimado para completar esta lección: **15 minutos**  
  
## Requisitos previos  
Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 11: Crear particiones](../analysis-services/lesson-11-create-partitions.md).  
  
## Crear roles  
  
#### Para crear un rol de usuario Administrador de ventas  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], haga clic en el menú **Modelo** y, luego, en **Roles**.  
  
2.  En el cuadro de diálogo **Administrador de roles** , haga clic en **Nuevo**.  
  
    Se agrega a la lista un nuevo rol con el permiso Ninguno.  
  
3.  Haga clic en el nuevo rol y, en la columna **Nombre**, cambie el nombre del rol a **Administrador de ventas por Internet**.  
  
4.  En la columna **Permisos**, haga clic en la lista desplegable y, después, seleccione el permiso **Lectura**.  
  
5.  Opcional: Haga clic en la pestaña **Miembros** y, después, en **Agregar**.  
  
6.  En el cuadro de diálogo **Seleccionar usuario o grupo**, especifique los usuarios o grupos de Windows de su organización que quiera incluir en el rol.  
  
7.  Compruebe las opciones seleccionadas y, después, haga clic en **Aceptar**  
  
#### Para crear un rol de usuario Analista de ventas EE. UU.  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], haga clic en el menú **Modelo** y, luego, en **Roles**.  
  
2.  En el cuadro de diálogo **Administrador de roles** , haga clic en **Nuevo**.  
  
    Se agrega a la lista un nuevo rol con el permiso Ninguno.  
  
3.  Haga clic en el nuevo rol y, en la columna **Nombre**, cambie el nombre del rol a **Ventas por Internet EE. UU**.  
  
4.  En la columna **Permisos**, haga clic en la lista desplegable y, después, seleccione el permiso **Lectura**.  
  
5.  Haga clic en la pestaña Filtros de fila y, después, solo para la tabla **Geografía**, en la columna de Filtro DAX, escriba la siguiente fórmula:  
  
    **=Geografía[código de país o región] = "US"**  
  
    Una fórmula de filtro de fila se debe resolver como un valor booleano (TRUE o FALSE). Con esta fórmula, está especificando que solo las filas con el valor de código de país o región de "US" estarán visibles para el usuario.  
  
    Cuando termine de crear la fórmula, presione ENTRAR.  
  
6.  Opcional: Haga clic en la pestaña **Miembros** y, después, en **Agregar**.  
  
7.  En el cuadro de diálogo **Seleccionar usuario o grupo**, especifique los usuarios o grupos de Windows de su organización que quiera incluir en el rol.  
  
8.  Compruebe las opciones seleccionadas y, después, haga clic en **Aceptar**  
  
#### Para crear un rol Administrador  
  
1.  En el cuadro de diálogo **Administrador de roles** , haga clic en **Nuevo**.  
  
2.  Haga clic en el nuevo rol y, en la columna **Nombre**, cambie el nombre del rol a **Administrador de ventas por Internet**.  
  
3.  En la columna **Permisos**, haga clic en la lista desplegable y luego seleccione el permiso **Administrador**.  
  
4.  Haga clic en la pestaña **Miembros** y luego en **Agregar**.  
  
5.  Opcional: En el cuadro de diálogo **Seleccionar usuario o grupo**, especifique los usuarios o grupos de Windows de su organización que quiera incluir en el rol.  
  
6.  Compruebe las opciones seleccionadas y, después, haga clic en **Aceptar**  
  
## Pasos siguientes  
Para continuar este tutorial, vaya a la lección siguiente: [Lección 13: Analizar en Excel](../analysis-services/lesson-13-analyze-in-excel.md).  
  
  
  
