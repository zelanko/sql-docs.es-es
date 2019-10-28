---
title: Modificación de claves principales | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- modifying primary keys
- primary keys [SQL Server], modifying
ms.assetid: 8e2a15ba-1cd1-4408-b860-16c3ee37d635
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ef278fbdc9fa2599e7612cd9c3b54b909a9bf1f0
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907317"
---
# <a name="modify-primary-keys"></a>Modificar claves principales
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , una clave principal puede modificarse mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Puede modificar la clave principal de una tabla si cambia el orden de las columnas, el nombre del índice, la opción agrupada o el factor de relleno.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para modificar una clave principal con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la tabla.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-modify-a-primary-key"></a>Para modificar una clave principal  
  
1.  Abra el Diseñador de tablas de la tabla cuya clave principal quiere modificar; después, haga clic con el botón derecho en el Diseñador de tablas y elija **Índices o claves** en el menú contextual.  
  
2.  En el cuadro de diálogo **Índices o claves** , seleccione el índice de clave principal en la lista **Índice o clave Primary/Unique seleccionados** .  
  
3.  Complete una de las acciones descritas en la tabla siguiente:  
  
    |A|Siga estos pasos|  
    |--------|------------------------|  
    |Cambiar el nombre de la clave principal|Escriba un nuevo nombre en el cuadro **Nombre** . Asegúrese de que el nuevo nombre no está duplicado en la lista **Índice o clave Primary/Unique seleccionados** .|  
    |Establecer la opción de índice clúster|Para crear un índice agrupado para la clave principal, seleccione **Crear como CLUSTERED**y seleccione la opción en el cuadro de lista desplegable. Solo puede existir un índice clúster por tabla. Si esta opción no está disponible para el índice, antes de nada debe desactivar esta configuración en el índice clúster existente.<br /><br /> Si no está seleccionada esta opción, se crea un índice no agrupado único.|  
    |Definir un factor de relleno|Expanda la categoría **Especificación de relleno** y escriba un número entero de 0 a 100 en el cuadro **Factor de relleno** . Para obtener más información sobre los factores de relleno y sus usos, vea [Especificar el factor de relleno para un índice](../../relational-databases/indexes/specify-fill-factor-for-an-index.md).|  
    |Cambiar el orden de las columnas|Haga clic en **Columnas** y, después, haga clic en los puntos suspensivos **(...)** situados a la derecha de la propiedad. En el cuadro de diálogo  **Columnas de índice** , quite las columnas de la clave principal. A continuación, vuelva a agregar las columnas en el orden que desee. Para quitar una columna de la clave, solo tiene que quitar el nombre de la columna de la lista **Nombre de columna** .|  
  
4.  En el menú **Archivo** , haga clic en **Guardar**_table name_.  

##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para modificar una clave principal**  
  
 Para modificar una restricción PRIMARY KEY mediante Transact-SQL, primero debe eliminar la restricción PRIMARY KEY existente y, a continuación, vuelva a crearla con la nueva definición. Para obtener más información, consulte [Delete Primary Keys](../../relational-databases/tables/delete-primary-keys.md) y [Create Primary Keys](../../relational-databases/tables/create-primary-keys.md).  
  
###  <a name="TsqlExample"></a>  
