---
title: Obtener acceso a tipos definidos por el usuario en ADO.NET | Microsoft Docs
description: Los UDT, escritos en .NET Framework lenguajes CLR, permiten a una base de datos SQL Server almacenar objetos y estructuras de datos personalizadas. En ADO.NET, un proveedor expone UDT.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- UDTs [CLR integration], ADO.NET
- user-defined types [CLR integration], ADO.NET
ms.assetid: 4b0d876c-8066-490e-8e18-327c0e942b19
author: rothja
ms.author: jroth
ms.openlocfilehash: cbbff72ab506238ec2134da8a91f91e3a315eb3f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727852"
---
# <a name="accessing-user-defined-types-in-adonet"></a>Obtener acceso a tipos definidos por el usuario en ADO.NET
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Los tipos definidos por el usuario (UDT) se escriben utilizando cualquiera de los lenguajes admitidos por el [!INCLUDE[msCoName](../../includes/msconame-md.md)] Common Language Runtime de .NET Framework (CLR) que produce código comprobable. Esto incluye [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# y [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic. Los UDT permiten almacenar objetos y estructuras de datos personalizadas en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los datos se exponen como miembros públicos de una clase o estructura de .NET Framework y los comportamientos se definen mediante métodos de la clase o estructura. Un UDT puede usarse como la definición de columna de una tabla, como una variable de un lote [!INCLUDE[tsql](../../includes/tsql-md.md)] o como un argumento de una función o procedimiento almacenado [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 En ADO.NET, el proveedor **System. Data. SqlClient** expone los UDT de las siguientes maneras:  
  
-   A través de **System. Data. SqlClient. SqlDataReader** como un objeto.  
  
-   A través de **SqlDataReader** como bytes sin formato.  
  
-   Como parámetro de un objeto **System. Data. SqlClient. SqlParameter** .  
  
## <a name="in-this-section"></a>En esta sección  
 [Recuperar datos UDT](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-retrieving-udt-data.md)  
 Describe cómo recuperar los datos UDT y cómo especificar parámetros.  
  
 [Actualizar columnas de UDT con DataAdapters](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-updating-udt-columns-with-dataadapters.md)  
 Describe cómo trabajar con UDT en **conjuntos** de datos y cómo actualizar datos UDT mediante **DataAdapters**.  
  
## <a name="see-also"></a>Consulte también  
 [Tipos CLR definidos por el usuario](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
