---
title: Acceso a los tipos definidos por el usuario en ADO.NET Microsoft Docs
description: Los UDT, escritos en lenguajes CLR de .NET Framework, permiten que una base de datos de SQL Server almacene objetos y estructuras de datos personalizadas. En ADO.NET, un proveedor expone UDT.
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
ms.openlocfilehash: d14205a6fb506f5d4fddaac1ab601ff1ee9205b8
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488266"
---
# <a name="accessing-user-defined-types-in-adonet"></a>Obtener acceso a tipos definidos por el usuario en ADO.NET
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Los tipos definidos por el usuario (UDT) se [!INCLUDE[msCoName](../../includes/msconame-md.md)] escriben con cualquiera de los lenguajes admitidos por Common Language Runtime (CLR) de .NET Framework que producen código comprobable. Esto incluye [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# y [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic. Los UDT permiten almacenar objetos y estructuras de datos personalizadas en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los datos se exponen como miembros públicos de una clase o estructura de .NET Framework y los comportamientos se definen mediante métodos de la clase o estructura. Un UDT puede usarse como la definición de columna de una tabla, como una variable de un lote [!INCLUDE[tsql](../../includes/tsql-md.md)] o como un argumento de una función o procedimiento almacenado [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 En ADO.NET, el proveedor **System.Data.SqlClient** expone los UDT de las siguientes maneras:  
  
-   A través de **System.Data.SqlClient.SqlDataReader** como un objeto.  
  
-   A través de **SqlDataReader** como bytes sin procesar.  
  
-   Como parámetro de un **System.Data.SqlClient.SqlParameter** objeto.  
  
## <a name="in-this-section"></a>En esta sección  
 [Recuperar datos UDT](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-retrieving-udt-data.md)  
 Describe cómo recuperar los datos UDT y cómo especificar parámetros.  
  
 [Actualizar columnas de UDT con DataAdapters](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-updating-udt-columns-with-dataadapters.md)  
 Describe cómo trabajar con UDT en **dataSets** y cómo actualizar datos UDT mediante **DataAdapters**.  
  
## <a name="see-also"></a>Consulte también  
 [Tipos CLR definidos por el usuario](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
