---
title: Asignación de bases de datos de origen y de destino (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- database schemas
- mapping, databases
- schemas, mapping to
- schemas, SQL Azure
- schemas, SQL Server
- source database
- target database
ms.assetid: 69bee937-7b2c-49ee-8866-7518c683fad4
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 192db2e6c074305ca258d76652351175c8a82751
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67907157"
---
# <a name="mapping-source-and-target-databases-accesstosql"></a>Asignación de bases de datos de origen y de destino (AccessToSQL)
Al conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, debe especificar una base de datos de destino para la migración. Si tiene varias bases de datos de Access, puede asignarlas a varias [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bases de datos (o esquemas) o a varios esquemas en la base de datos de SQL Azure conectada.  
  
## <a name="sql-server-or-sql-azure-database-schemas"></a>Esquemas de base de datos SQL Server o SQL Azure  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]las bases de datos usan el concepto de esquemas para separar los objetos de una base de datos en grupos lógicos. Por ejemplo, una base de datos de biblioteca podría usar tres esquemas denominados **libros**, **audio**y **vídeo** para separar los objetos de libro, audio y vídeo entre sí. De forma predeterminada, la base de datos de Access se asigna a la base [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de datos **maestra** y al esquema **DBO** en y a la base de datos conectada y al esquema **DBO** en SQL Azure.  
  
A menos que personalice la asignación entre cada base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de Access y la base de datos y el esquema, SSMA migrará todos los esquemas y datos asociados a la base de datos de Access a la base de datos predeterminada asignada.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modificar la base de datos y el esquema de destino  
SSMA le permite asignar cada base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de Access a o SQL Azure base de datos y esquema. En el procedimiento siguiente se describe cómo personalizar la asignación por base de datos.  
  
**Para modificar la base de datos y el esquema de destino**  
  
1.  En el panel Explorador de metadatos de acceso, seleccione **acceso-metadatos**.  
  
    La asignación de esquemas también está disponible cuando se selecciona el nodo **bases** de datos o cualquier nodo de base de datos. La lista de asignación de esquemas está personalizada para el objeto seleccionado.  
  
2.  En el panel derecho, haga clic en la pestaña **asignación de esquema** .  
  
    Verá una tabla que contiene los nombres de las bases de datos de Access y su esquema de ssNoVersion o SQL Azure correspondiente. El esquema de destino se denota en una notación de dos partes (Database. Schema).  
  
3.  Seleccione la fila que contiene la asignación que desea personalizar y, a continuación, haga clic en **modificar**.  
  
4.  En el cuadro de diálogo **elegir esquema de destino** , puede buscar el esquema y la base de datos de destino disponibles o escribir la base de datos y el nombre de esquema en el cuadro de texto en una notación de dos partes (Database. Schema) y, a continuación, hacer clic en **Aceptar**.  
  
**Modos de asignación**  
  
-   Asignar a SQL Server  
  
Puede asignar una base de datos de origen a cualquier base de datos de destino. De forma predeterminada, la base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de origen se asigna a la base de datos de destino con la que se ha conectado mediante SSMA. Si la base de datos de destino que se está [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]asignando no existe en, se le mostrará un mensaje que indica que la base de datos o **el esquema no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] existen en los metadatos de destino. Se creará durante la sincronización. ¿Desea continuar? "** Haga clic en Sí. Del mismo modo, puede asignar un esquema a un esquema no existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos de destino que se creará durante la sincronización.  
  
-   Asignar a SQL Azure  
  
Puede asignar la base de datos de origen a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos de destino conectada o a cualquier esquema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la base de datos de destino conectada. Si asigna un esquema de origen a cualquier esquema no existente en la base de datos de destino conectada, se le pedirá un mensaje que indica que el **esquema no existe en los metadatos de destino. Se creará durante la sincronización. ¿Desea continuar? "** Haga clic en sí.  
  
## <a name="reverting-to-your-initial-database-and-schema"></a>Revertir a la base de datos y el esquema iniciales  
Si personaliza la asignación entre una base de datos de Access [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y una o SQL Azure base de datos y esquema, puede revertir la asignación a la base de datos que especificó [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al conectarse a o SQL Azure.  
  
**Para restablecer la base de datos y el esquema predeterminados**  
  
1.  En la pestaña asignación de esquema, seleccione cualquier fila y haga clic en **Restablecer valores predeterminados** para revertir a la base de datos y el esquema predeterminados.  
  
## <a name="next-step"></a>siguiente paso  
El siguiente paso del proceso de migración consiste en [convertir objetos de base de datos](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>Consulte también  
[Migrar bases de datos de Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
