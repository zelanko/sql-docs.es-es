---
title: Modificación de restricciones UNIQUE | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- modifying constraints
- UNIQUE constraints [SQL Server], modifying
- constraints [SQL Server], modifying
- constraints [SQL Server], unique
ms.assetid: fddbdc9e-958b-4614-8e88-6ca205d64a4e
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e195529fd339d6449ded94064076430aff9f1214
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37317975"
---
# <a name="modify-unique-constraints"></a>Modificar restricciones UNIQUE
  Puede modificar una restricción UNIQUE en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para modificar una restricción UNIQUE con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Requiere el permiso ALTER en la tabla.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-modify-a-unique-constraint"></a>Para modificar una restricción UNIQUE  
  
1.  En el **Explorador de objetos**, haga clic con el botón derecho en la tabla que contiene la restricción UNIQUE y seleccione **Diseño**.  
  
2.  En el menú **Diseñador de tablas** , haga clic en **Índices o claves…**.  
  
3.  En el cuadro de diálogo **Índices o claves** , en **Clave principal o única, o índice seleccionado**, seleccione la restricción que quiera modificar.  
  
4.  Complete una de las acciones descritas en la tabla siguiente:  
  
    |A|Siga estos pasos|  
    |--------|------------------------|  
    |Cambiar las columnas a las que está asociada la restricción|1) En la cuadrícula situada debajo de **(General)**, haga clic en **Columnas** y haga clic en los puntos suspensivos **(…)** que aparecen a la derecha de la propiedad.<br /><br /> 2) En el cuadro de diálogo **Columnas de índice** , especifique la nueva columna o criterio de ordenación (o ambos) del índice.|  
    |Cambiar el nombre de la restricción|En la cuadrícula situada debajo de **Identidad**, escriba un nuevo nombre en el cuadro **Nombre** . Asegúrese de que el nuevo nombre no esté duplicado en la lista **Clave principal o única, o índice seleccionado** .|  
    |Establecer la opción de índice clúster|En la cuadrícula situada debajo de **Diseñador de tablas**, seleccione **Crear como CLUSTERED** y, en el menú desplegable, elija Sí para crear un índice agrupado o No para crear un índice no agrupado. Solo puede existir un índice clúster por tabla. Si ya existe un índice clúster en esta tabla, deberá desactivar esta configuración en el índice original.|  
    |Definir un factor de relleno|En la cuadrícula situada debajo de **Diseñador de tablas**, expanda la categoría **Especificación de relleno** y escriba un entero de 0 a 100 en el cuadro **Factor de relleno** .|  
  
5.  En el menú **Archivo**, haga clic en **Guardar***nombre de tabla*.  
  
##  <a name="TsqlProcedure"></a> **Para modificar una restricción UNIQUE**  
  
 Para modificar una restricción UNIQUE mediante Transact-SQL, deberá eliminar la restricción UNIQUE existente y, a continuación, volver a crearla con la nueva definición. Para obtener más información, consulte [Delete Unique Constraints](delete-unique-constraints.md) y [Create Unique Constraints](create-unique-constraints.md).  
  
###  <a name="TsqlExample"></a>  
