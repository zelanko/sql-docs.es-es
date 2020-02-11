---
title: Modificación de restricciones UNIQUE | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- modifying constraints
- UNIQUE constraints [SQL Server], modifying
- constraints [SQL Server], modifying
- constraints [SQL Server], unique
ms.assetid: fddbdc9e-958b-4614-8e88-6ca205d64a4e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8bb3daf170e25abc9b346aeaedb4b835cae2dfdd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68809920"
---
# <a name="modify-unique-constraints"></a>Modificar restricciones UNIQUE
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
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-modify-a-unique-constraint"></a>Para modificar una restricción UNIQUE  
  
1.  En el **Explorador de objetos**, haga clic con el botón derecho en la tabla que contiene la restricción UNIQUE y seleccione **Diseño**.  
  
2.  En el menú **Diseñador de tablas**, haga clic en **Índices o claves...**.  
  
3.  En el cuadro de diálogo **Índices o claves** , en **Clave principal o única, o índice seleccionado**, seleccione la restricción que quiera modificar.  
  
4.  Complete una de las acciones descritas en la tabla siguiente:  
  
    |A|Siga estos pasos|  
    |--------|------------------------|  
    |Cambiar las columnas a las que está asociada la restricción|1) En la cuadrícula situada debajo de **(General)**, haga clic en **Columnas** y después en los puntos suspensivos **(...)** situados a la derecha de la propiedad.<br /><br /> 2) En el cuadro de diálogo **Columnas de índice** , especifique la nueva columna o criterio de ordenación (o ambos) del índice.|  
    |Cambiar el nombre de la restricción|En la cuadrícula situada debajo de **Identidad**, escriba un nuevo nombre en el cuadro **Nombre** . Asegúrese de que el nuevo nombre no esté duplicado en la lista **Clave principal o única, o índice seleccionado** .|  
    |Establecer la opción de índice clúster|En la cuadrícula situada debajo de **Diseñador de tablas**, seleccione **Crear como CLUSTERED** y, en el menú desplegable, elija Sí para crear un índice agrupado o No para crear un índice no agrupado. Solo puede existir un índice clúster por tabla. Si ya existe un índice clúster en esta tabla, deberá desactivar esta configuración en el índice original.|  
    |Definir un factor de relleno|En la cuadrícula situada debajo de **Diseñador de tablas**, expanda la categoría **Especificación de relleno** y escriba un entero de 0 a 100 en el cuadro **Factor de relleno** .|  
  
5.  En el menú **Archivo** , haga clic en **Guardar**_table name_.  
  
##  <a name="TsqlProcedure"></a>**Para modificar una restricción UNIQUE**  
  
 Para modificar una restricción UNIQUE mediante Transact-SQL, deberá eliminar la restricción UNIQUE existente y, a continuación, volver a crearla con la nueva definición. Para obtener más información, consulte [Delete Unique Constraints](delete-unique-constraints.md) y [Create Unique Constraints](create-unique-constraints.md).  
  
###  <a name="TsqlExample"></a>  
