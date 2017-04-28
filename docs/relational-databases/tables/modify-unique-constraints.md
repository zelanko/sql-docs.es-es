---
title: "Modificación de restricciones UNIQUE | Microsoft Docs"
ms.custom: 
ms.date: 10/12/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying constraints
- UNIQUE constraints [SQL Server], modifying
- constraints [SQL Server], modifying
- constraints [SQL Server], unique
ms.assetid: fddbdc9e-958b-4614-8e88-6ca205d64a4e
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2eb829d6362e39096134906442d6c4c0adf44f2a
ms.lasthandoff: 04/11/2017

---
# <a name="modify-unique-constraints"></a>Modificar restricciones UNIQUE
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Puede modificar una restricción UNIQUE en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para modificar una restricción UNIQUE con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la tabla.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-modify-a-unique-constraint"></a>Para modificar una restricción UNIQUE  
  
1.  En el **Explorador de objetos**, haga clic con el botón derecho en la tabla que contiene la restricción UNIQUE y seleccione **Diseño**.  
  
2.  En el menú **Diseñador de tablas** , haga clic en **Índices o claves…**.  
  
3.  En el cuadro de diálogo **Índices o claves** , en **Clave principal o única, o índice seleccionado**, seleccione la restricción que quiera modificar.  
  
4.  Complete una de las acciones descritas en la tabla siguiente:  
  
    |Para|Siga estos pasos|  
    |--------|------------------------|  
    |Cambiar las columnas a las que está asociada la restricción|1) En la cuadrícula situada debajo de **(General)**, haga clic en **Columnas** y haga clic en los puntos suspensivos **(…)** que aparecen a la derecha de la propiedad.<br /><br /> 2) En el cuadro de diálogo **Columnas de índice** , especifique la nueva columna o criterio de ordenación (o ambos) del índice.|  
    |Cambiar el nombre de la restricción|En la cuadrícula situada debajo de **Identidad**, escriba un nuevo nombre en el cuadro **Nombre** . Asegúrese de que el nuevo nombre no esté duplicado en la lista **Clave principal o única, o índice seleccionado** .|  
    |Establecer la opción de índice clúster|En la cuadrícula situada debajo de **Diseñador de tablas**, seleccione **Crear como CLUSTERED** y, en el menú desplegable, elija Sí para crear un índice agrupado o No para crear un índice no agrupado. Solo puede existir un índice clúster por tabla. Si ya existe un índice clúster en esta tabla, deberá desactivar esta configuración en el índice original.|  
    |Definir un factor de relleno|En la cuadrícula situada debajo de **Diseñador de tablas**, expanda la categoría **Especificación de relleno** y escriba un entero de 0 a 100 en el cuadro **Factor de relleno** .|  
  
5.  En el menú **Archivo** , haga clic en **Guardar***table name*.  
  
##  <a name="TsqlProcedure"></a> **Para modificar una restricción UNIQUE**  
  
 Para modificar una restricción UNIQUE mediante Transact-SQL, deberá eliminar la restricción UNIQUE existente y, a continuación, volver a crearla con la nueva definición. Para obtener más información, consulte [Delete Unique Constraints](../../relational-databases/tables/delete-unique-constraints.md) y [Create Unique Constraints](../../relational-databases/tables/create-unique-constraints.md).  
  
###  <a name="TsqlExample"></a>  

